

	struct Node 
	{ 
		int key; 
		std::string value; 
		Node* next; 
		
		Node(int k, const std::string& v) 
			: key(k), value(v), next(nullptr) 
		{
		} 
	};
		
	class HashTable
	{
	public:
		HashTable() 
			: HashTable(std::random_device{}()) 
		{
		}
		
		// seed lets you reproduce a run 
		explicit HashTable(std::uint64_t seed) 
		{ 
			std::mt19937_64 gen(seed); 
			a = std::uniform_int_distribution<std::uint64_t>(1, prime - 1)(gen); 
			b = std::uniform_int_distribution<std::uint64_t>(0, prime - 1)(gen); 
		}
		
		~HashTable() 
		{ 
			for (int i = 0; i < buckets; ++i) 
			{ 
				Node* current = table[i]; 
				while (current != nullptr) 
				{ 
					Node* next = current->next; 
					delete current; 
					current = next; 
				} 
			} 
		}
		
		HashTable(const HashTable&) = delete; 
		HashTable& operator=(const HashTable&) = delete;
		
		int hashIndex(int key) const // keys must be nonnegative 
		{ 
			std::uint64_t k = static_cast<std::uint64_t>(key); 
			return static_cast<int>(((a * k + b) % prime) % buckets); 
		}
		
		std::string search(int key) const 
		{ 
			Node* current = table[hashIndex(key)]; 
			while (current != nullptr) 
			{ 
				if (current->key == key) 
					return current->value; 
					
				current = current->next; 
			} 
			return "NOT FOUND"; 
		}
		
		void insert(int key, const std::string& value) 
		{ 
			int index = hashIndex(key); 
			Node* head = table[index]; 
			for (Node* current = head; 
				current != nullptr; current = current->next) 
				
			{ 
				if (current->key == key) 
				{ 
					current->value = value; 
					return; 
				} 
			} 
			
			Node* newNode = new Node(key, value); 
			newNode->next = head; 
			table[index] = newNode; 
		}
		
		void remove(int key) 
		{ 
			int index = hashIndex(key); 
			Node* current = table[index]; 
			Node* prev = nullptr; 
			while (current != nullptr) 
			{ 
				if (current->key == key) 
				{ 
					if (prev == nullptr) 
						table[index] = current->next;
					else 
						 prev->next = current->next;
						 
					delete current; 
					return; 
				} 
				prev = current; 
				current = current->next; 
			} 
		}
		
	private: 
		static constexpr int buckets = 11; 
		static constexpr std::uint64_t prime = 4294967291ULL; // largest prime below 2^32 
		
		std::uint64_t a; 
		std::uint64_t b; 
		Node* table[buckets]{};
	};
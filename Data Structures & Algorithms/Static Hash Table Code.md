

	struct Node
	{
		int key;
		std::string value;
		Node* next;
		
		Node(int k, const std::string& v) 
			: key(k), value(v), next(nullptr) 
		{
		}
	}

	class HashTable
	{
	public:
		HashTable()  
		{
		}
		
		HashTable(const HashTable&) = delete; 
		HashTable& operator=(const HashTable&) = delete;
			
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
		 
			
			
		int hashIndex(int key) //get hash index
		{
			return ((key % buckets) + buckets) % buckets;
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
		void insert(int key, std::string& value) //inserting the data to a bucket
		{
			 int index = hashIndex(key);  // key % value
			 
			 Node* head = table[index];
			 Node* current = head;
			
			while (current != nullptr)
			{
				if (current->key == key)
				{
					current->value = value;
					return;
				}
				current = current->next;
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
		static constexpr int buckets = 10;
		Node* table[buckets];
	}
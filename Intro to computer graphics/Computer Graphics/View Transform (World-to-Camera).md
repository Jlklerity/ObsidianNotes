
![[Pasted image 20260723123352.png]]

![[Pasted image 20260723123228.png]]
## $$M_{w \rightarrow v} = \begin{bmatrix} u_x & u_y & u_z & -\vec{u} \cdot E^w \\ v_x & v_y & v_z & -\vec{v} \cdot E^w \\ w_x & w_y & w_z & -\vec{w} \cdot E^w \\ 0 & 0 & 0 & 1 \end{bmatrix}$$


`view_xform = glm::lookAt(CORE10::camera_pos, CORE10::camera_target,` 
					`CORE10::camera_up);`
												 
`• eye = CORE10::camera_pos (Where the camera is sitting)`
`• center = CORE10::camera_target (What the camera is pointing at)`
`• up = CORE10::camera_up (Which way is straight up)`


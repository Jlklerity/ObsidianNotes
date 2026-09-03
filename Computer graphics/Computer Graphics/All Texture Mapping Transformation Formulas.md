
### Window-To-Viewport (Bounding Box) Mapping

> [!info]
> Use this when mapping a model's 2D bounding box (source) to a specific target rectangle on a texture map.

Calculate Scale (S): The ratio of the target dimensions to the source dimensions.

$$
Sx= \frac{\text{Target Width}}{\text{Source Width}}, \quad S_y = \frac{\text{Target Height}}{\text{Source Height}}​
$$

### Texture-To-Texel Coordinates

$$
(S,T)=(s⋅w,t⋅h)​
$$
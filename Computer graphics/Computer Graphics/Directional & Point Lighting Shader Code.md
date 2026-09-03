
## Using Phong Shading as example

`//Directional Light vertex shader code:`
`#version 300 es`
`// Vertex information`
`layout(location = 0) in vec4  VertexPosition;`
`layout(location = 1) in vec3  Normal;`

`// Model View Project matrix`
`uniform mat4    ModelViewProjectionMatrix;`
`uniform mat4    ModelViewMatrix;`
`uniform mat3    NormalMatrix;`

`out vec3    normalCoord;`
`out vec3    eyeCoord;`

`void main()` 
`{`
    `normalCoord = NormalMatrix * Normal;`
    `eyeCoord    = vec3 ( ModelViewMatrix * VertexPosition );`
    `gl_Position = ModelViewProjectionMatrix * VertexPosition;`
`}`

`//Directional Light fragment shader code:`
`#version 300 es`
`precision mediump float;`

`// Material property`
`uniform vec3    MaterialAmbient;`
`uniform vec3    MaterialSpecular;`
`uniform vec3    MaterialDiffuse;`

`// Light property`
`uniform vec3    LightAmbient;`
`uniform vec3    LightSpecular;`
`uniform vec3    LightDiffuse;`

`uniform vec3    LightPosition;`
`uniform float   ShininessFactor;`

`in vec3    normalCoord;`
`in vec3    eyeCoord;`

`layout(location = 0) out vec4 FinalColor;`

`vec3 normalizeNormal, normalizeEyeCoord, normalizeLightVec, V, R, ambient, diffuse, specular;`
`float sIntensity, cosAngle;`

`vec3 PhongShading()`
`{`
    `normalizeNormal   = normalize( normalCoord );`
    `normalizeEyeCoord = normalize( eyeCoord );`
    `normalizeLightVec = normalize( LightPosition ); //directional lighting mode`
  `//normalizeLightVec = normalize( LightPosition - eyeCoord );` 
																							`// true position this time`
																							`//for point lighting mode`
    
    // Diffuse Intensity
    cosAngle = max( 0.0, dot( normalizeNormal, normalizeLightVec ));

    // Specular Intensity
    V = -normalizeEyeCoord; // Viewer's vector
    R = reflect( -normalizeLightVec, normalizeNormal );
    sIntensity = pow( max( 0.0, dot( R, V ) ), ShininessFactor ); // Reflectivity

    // ADS color as result of Material & Light interaction
    ambient    = MaterialAmbient  * LightAmbient;
    diffuse    = MaterialDiffuse  * LightDiffuse;
    specular   = MaterialSpecular * LightSpecular;

    return ambient + ( cosAngle * diffuse ) + ( sIntensity * specular );
}

`void main() {`
  `FinalColor = vec4(PhongShading(), 1.0);`
`}`


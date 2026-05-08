Previous: [Torus](modeling.md)


# Building Torus

Este método consiste em criar um círculo inicial no plano XY à uma certa distância da origem no eixo x (```inner```) e no eixo y (```outer```). Então, este círculo é rotacionado em torno do eixo y, gerando novos círculos até formar um torus.

Algoritmo para criar o círculo incial no plano XY:

 ```
    for (size_t i = 0; i < precision + 1; i++) {
        float angle = i * 360.0f / (float)precision;
        matrix rotateMatrix = rotate(0.0f, 0.0f, angle);


        // vertex position
        vec3 vertexPosition = rotateMatrix * vec3(0.0f, outer, 0.0f);
        vertexPosition = vertexPosition + vec3(inner, 0.0f, 0.0f);

        // texture coordinates
        float u = 0.0f;
        float v = (float)i / float(precision);

        // st tangent
        matrix rotateTangent = kengine::rotate(0.0f, 0.0f, angle + 90.0f);
        vec3 tTangent = rotateTangent * vec3(0.0f, -1.0f, 0.0f);
        vec3 sTangent = rotateTangent * vec3(0.0f, 0.0f, -1.0f);
        
        // normal
        vec3 normal = crossProduct(tTangent, sTangent);
    }
 ```

 Algoritmo para criar ```n``` círculos adicionais rotacionando o círculo inicial em torno do eixo Y.

 ```
    for (size_t ring = 1; ring < precision + 1; ring++) {
        for (size_t vert = 0; vert < precision + 1; vert++) {
            float angle = (float)ring * 360.0f / (float)precision;
            matrix rotateMatrix = rotate(0.0f, angle, 0.0f);

            // vertex position
            vec3 newVertex = rotateMatrix * getVertexOfFirstCircle(vert);

            // texture coordinates
            float u = float(ring) * 2.0f / float(precision);
            float v = getTextureCoordinateOfFirstCircle[vert].t;

            // st tangent
            vec3 sTangent = rotateMatrix * getsTangentOfFirstCircle(vert);
            vec3 tTangent = rotateMatrix * gettTangentOfFirstCircle(vert);

            // normal
            vec3 n = rotateMatrix * getNormalOfFirstCircle();
        }
    }
 ```

Este método mapea a textura até a metade horizontal da esfeta e depois repete para outra a metade. Para fazer isso, geramos as coordenadas para o eixo u de 0.0 á 2.0 porque o mapeamento vai de 0.0 a 1.0. Se estiver utilizando OpenGL, é necessário também configurar o mapeamento para repetir a textura com ```GL_REPEAT```.

 
 Algoritmo para gerar indices do torus:

 ```
    std::vector<GLushort> indices;
 	for (int ring = 0; ring < precision; ring++) {
		for (int vert = 0; vert < precision; vert++) {

			GLushort row = ring * (precision + 1);
			GLushort next_row = (ring + 1) * (precision + 1);

			// first triangle (CCW visto de fora)
			indices.push_back(row + vert);
			indices.push_back(next_row + vert);
			indices.push_back(row + vert + 1);
			// second triangle
			indices.push_back(row + vert + 1);
			indices.push_back(next_row + vert);
			indices.push_back(next_row + vert + 1);
		}
	}
 ```


# References

- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.
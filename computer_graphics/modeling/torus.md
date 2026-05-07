Previous: [Torus](modeling.md)


# Building Torus

Este método consiste em criar um círculo inicial no plano XY à uma certa distância da origem no eixo x (```inner```) e no eixo y (```outer```). Então, este círculo é rotacionado em torno do eixo y, gerando novos círculos até formar um torus.

Algoritmo para criar o círculo incial no plano XY:

 ```
    for (size_t i = 0; i < precision + 1; i++) {
        float angle = i * 360.0f / (float)precision;
        matrix rotateMatrix = rotate(0.0f, 0.0f, angle);

        vec3 vertexPosition = r * vec3(0.0f, outer, 0.0f);
        vertexPosition = vertexPosition + vec3(inner, 0.0f, 0.0f);

        // vertex position
        float x = vertexPosition.x;
        float y = vertexPosition.y;
        float z = vertexPosition.z;

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
			float angle = (float)ring * 360.0f / (float)precision);
			matrix r = rotate(0.0f, angle, 0.0f);

            vec3 vertexOfFirstCircle = getVertexOfFirstCircle(vert);
			vec3 newVertex = r * vertexOfFirstCircle;

            float x = newVertex.x;
            float y = newVertex.y;
            float z = newVertex.z;

            // texture coordiantes
			float u = float(ring) * 2.0f / float(precision); // considera de 0 a 2.0 (necessário utilizar GL_REPEAT)
			float v = getTextureCoordinateOfFirstCircle[vert].t;

			r = rotate(0.0f, angle, 0.0f);

			vec3 sTangent = r * getsTangentOfFirstCircle(vert);
			vec3 tTangent = r * gettTangentOfFirstCircle(vert);
			vec3 n = r * getNormalOfFirstCircle();
		}
	}
 ```


# References

- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.
Previous: [Game Development](game_dev.md)

# Camera Control


# First Person Camera control

```
    void onMouseMotionEvent(const int x, const int y)
    {
        if (isMouseButtonPressed) {
            xoffset = x - m_mouseXpos;
            yoffset = m_mouseYpos - y;

            yaw += (xoffset * sensitivity); // sensitivity == 0.1f
            yaw = std::fmod(yaw, 360.0f); // yaw constrains
            pitch += (yoffset * sensitivity * 0.1f);

            // pitch constrains
            if (pitch > 89.0f)
                pitch = 89.0f;

            if (pitch < -89.0f)
                pitch = -89.0f;

            forward.x = std::cos(yaw * ANGLE_TO_RADIAN_CONSTANT) * std::cos(pitch);
            forward.y = std::sin(pitch);
            forward.z = std::sin(yaw * ANGLE_TO_RADIAN_CONSTANT) * std::cos(pitch);
            forward.normalize();

            camera.center = eye + forward;
            // set uniform here (view matrix is lookAt(camera))
        }

        m_mouseXpos = x;
        m_mouseYpos = y;
    }
```

```
    void onMouseButtonEvent(const int button, const int state, const int x, const int y)
    {
        if (button == MOUSE::LEFT) {
            isMouseButtonPressed = state == MOUSE::DOWN ? true : false; 
        }
    }
```


# References

- GORDON, V. S. CLEVENGER, J. Computer Graphics Programming in OpenGL with C++, 3rd ed. Mercury Learning and Information, 2024.  
- LearnOpenGL - Camera. Available in [https://learnopengl.com/Getting-started/Camera](https://learnopengl.com/Getting-started/Camera).   
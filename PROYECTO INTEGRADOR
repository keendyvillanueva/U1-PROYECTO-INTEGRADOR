# U1-PROYECTO-INTEGRADOR
ESCENARIO PROCEDURAL
CODIGO
import bpy
import math

# --------------------------------
# LIMPIAR ESCENA
# --------------------------------
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete(use_global=False)

# --------------------------------
# CREAR CURVA CAMINO
# --------------------------------
bpy.ops.curve.primitive_bezier_curve_add()
curve = bpy.context.object
curve.name = "Camino"
curve.data.dimensions = '3D'

# Editar curva
spline = curve.data.splines[0]
spline.bezier_points.add(4)

for i, point in enumerate(spline.bezier_points):
    x = i * 6
    y = math.sin(i * 1.3) * 5
    z = 0
    point.co = (x, y, z)
    point.handle_left_type = 'AUTO'
    point.handle_right_type = 'AUTO'

# --------------------------------
# CREAR UN BLOQUE BASE
# --------------------------------
bpy.ops.mesh.primitive_cube_add(size=2)
bloque = bpy.context.object
bloque.name = "Bloque"

# --------------------------------
# MODIFICADOR ARRAY
# --------------------------------
array = bloque.modifiers.new(name="Array", type='ARRAY')
array.count = 30
array.relative_offset_displace[0] = 1.1

# --------------------------------
# MODIFICADOR CURVE
# --------------------------------
curve_mod = bloque.modifiers.new(name="Curve", type='CURVE')
curve_mod.object = curve
curve_mod.deform_axis = 'POS_X'

# --------------------------------
# CREAR CÁMARA
# --------------------------------
bpy.ops.object.camera_add(location=(0, -10, 5))
camera = bpy.context.object

# Constraint FOLLOW PATH
follow = camera.constraints.new(type='FOLLOW_PATH')
follow.target = curve
follow.use_curve_follow = True

# --------------------------------
# ANIMACIÓN
# --------------------------------
curve.data.path_duration = 200
follow.offset_factor = 0
camera.constraints["Follow Path"].keyframe_insert(data_path="offset_factor", frame=1)

follow.offset_factor = 1
camera.constraints["Follow Path"].keyframe_insert(data_path="offset_factor", frame=200)

# Hacer cámara activa
bpy.context.scene.camera = camera

print("Simulación lista! Presiona Play.")



import bpy
import math

# ----------------------------
# LIMPIAR ESCENA
# ----------------------------
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete(use_global=False)

# ----------------------------
# CREAR CURVA
# ----------------------------
bpy.ops.curve.primitive_bezier_curve_add()
curve = bpy.context.object
curve.name = "Camino"
curve.data.dimensions = '3D'

spline = curve.data.splines[0]
spline.bezier_points.add(4)

for i, point in enumerate(spline.bezier_points):
    x = i * 6
    y = math.sin(i * 1.2) * 5
    z = 0
    point.co = (x, y, z)
    point.handle_left_type = 'AUTO'
    point.handle_right_type = 'AUTO'

# ----------------------------
# CREAR BLOQUE BASE
# ----------------------------
bpy.ops.mesh.primitive_cube_add(size=2)
bloque = bpy.context.object
bloque.name = "Bloque"

# Escalar para que parezca pasillo
bloque.scale[1] = 2
bloque.scale[2] = 2

# ----------------------------
# ARRAY (repetición)
# ----------------------------
array = bloque.modifiers.new(name="Array", type='ARRAY')
array.count = 40
array.relative_offset_displace[0] = 1.1

# ----------------------------
# CURVE MODIFIER
# ----------------------------
curve_mod = bloque.modifiers.new(name="Curve", type='CURVE')
curve_mod.object = curve
curve_mod.deform_axis = 'POS_X'

# ----------------------------
# CREAR CÁMARA
# ----------------------------
bpy.ops.object.camera_add(location=(0, -8, 4))
camera = bpy.context.object

# Constraint FOLLOW PATH
follow = camera.constraints.new(type='FOLLOW_PATH')
follow.target = curve
follow.use_curve_follow = True

# Orientación correcta
follow.forward_axis = 'FORWARD_Y'
follow.up_axis = 'UP_Z'

# ----------------------------
# ANIMACIÓN
# ----------------------------
curve.data.path_duration = 250

follow.offset_factor = 0
follow.keyframe_insert(data_path="offset_factor", frame=1)

follow.offset_factor = 1
follow.keyframe_insert(data_path="offset_factor", frame=250)

# Cámara activa
bpy.context.scene.camera = camera

print("Simulación lista. Presiona Play.")

import bpy
import math

# LIMPIAR
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

# CREAR CURVA
bpy.ops.curve.primitive_bezier_curve_add()
curve = bpy.context.object
curve.name = "Camino"

spline = curve.data.splines[0]
spline.bezier_points.add(4)

for i, point in enumerate(spline.bezier_points):
    point.co = (i*5, math.sin(i)*4, 0)
    point.handle_left_type = 'AUTO'
    point.handle_right_type = 'AUTO'

# ACTIVAR PATH
curve.data.path_duration = 250
curve.data.use_path = True

# CREAR BLOQUE
bpy.ops.mesh.primitive_cube_add(size=2)
bloque = bpy.context.object

array = bloque.modifiers.new("Array", 'ARRAY')
array.count = 30
array.relative_offset_displace[0] = 1.1

curve_mod = bloque.modifiers.new("Curve", 'CURVE')
curve_mod.object = curve
curve_mod.deform_axis = 'POS_X'

# CREAR CÁMARA
bpy.ops.object.camera_add(location=(0, -5, 5))
camera = bpy.context.object

# FOLLOW PATH
constraint = camera.constraints.new(type='FOLLOW_PATH')
constraint.target = curve
constraint.use_curve_follow = True
constraint.forward_axis = 'FORWARD_Y'
constraint.up_axis = 'UP_Z'

# 🔥 ESTA LÍNEA ES LA CLAVE
bpy.ops.object.select_all(action='DESELECT')
camera.select_set(True)
bpy.context.view_layer.objects.active = camera
bpy.ops.constraint.followpath_path_animate(constraint=constraint.name)

# Cámara activa
bpy.context.scene.camera = camera

print("Ahora sí se mueve. Presiona Play.")

DESCRIPCION
Introducción:
Este proyecto demuestra cómo crear una animación en Blender donde una cámara sigue un camino curvo, mientras que una serie de objetos (en este caso, cubos escalados para simular un pasillo) se extienden a lo largo de ese mismo camino. Se utilizan modificadores de Array y Curve para lograr este efecto. El objetivo es mostrar el uso de herramientas de animación de Blender para crear un movimiento de cámara dinámico y la generación procedural de geometría.
Pasos:
Limpieza de la Escena:
Primero, se eliminan todos los objetos preexistentes en la escena de Blender para comenzar con un lienzo limpio. Esto se realiza seleccionando todos los objetos (bpy.ops.object.select_all(action='SELECT')) y luego eliminándolos (bpy.ops.object.delete()).
Creación de la Curva (Camino):
Se crea una curva Bezier primitiva (bpy.ops.curve.primitive_bezier_curve_add()) que servirá como el camino que seguirá la cámara y los objetos.
Se nombra la curva como "Camino" para facilitar su identificación en la escena.
Se ajusta la forma de la curva añadiendo puntos Bezier y modificando sus coordenadas en el espacio 3D para crear una forma sinusoidal (math.sin(i * 1.1) * 4). Los manejadores de los puntos Bezier se configuran en modo 'AUTO' para suavizar las transiciones.
Se activa la animación de path en la curva (curve.data.use_path = True) y se define la duración del recorrido (curve.data.path_duration = 250).
Creación del Bloque Base:
Se añade un cubo primitivo (bpy.ops.mesh.primitive_cube_add(size=2)) que actuará como el bloque base para la repetición a lo largo del camino.
Se escala el cubo en los ejes Y y Z para darle la forma de un pasillo (bloque.scale[1] = 2, bloque.scale[2] = 2).
Modificador Array:
Se añade un modificador Array al bloque (bloque.modifiers.new(name="Array", type='ARRAY')).
Se configura el modificador para crear 30 copias del bloque (array.count = 30).
Se ajusta el desplazamiento relativo entre las copias en el eje X (array.relative_offset_displace[0] = 1.1) para crear un espacio entre los bloques.
Modificador Curve:
Se añade un modificador Curve al bloque (bloque.modifiers.new(name="Curve", type='CURVE')).
Se establece la curva "Camino" como el objeto que deformará el array de bloques (curve_mod.object = curve).
Se define el eje de deformación como el eje X (curve_mod.deform_axis = 'POS_X').
Creación de la Cámara:
Se añade una cámara a la escena (bpy.ops.object.camera_add(location=(0, -8, 4))).
Constraint Follow Path:
Se añade un constraint Follow Path a la cámara (camera.constraints.new(type='FOLLOW_PATH')).
Se establece la curva "Camino" como el objetivo del constraint (follow.target = curve).
Se activa la opción "Use Curve Follow" para que la cámara se oriente según la curva (follow.use_curve_follow = True).
Se configuran los ejes de orientación para que la cámara apunte hacia adelante a lo largo del camino (follow.forward_axis = 'FORWARD_Y', follow.up_axis = 'UP_Z').
Animación:
Se selecciona la cámara y se la convierte en el objeto activo.
Se utiliza el operador bpy.ops.constraint.followpath_path_animate(constraint=follow.name) para animar automáticamente el offset de la cámara a lo largo del camino, creando keyframes que abarcan la duración definida en la curva (250 frames).
Cámara Activa:
Se establece la cámara creada como la cámara activa de la escena (bpy.context.scene.camera = camera).
Conclusión:
Este script demuestra la combinación de varias herramientas de Blender para crear una animación compleja de manera relativamente sencilla. El uso de modificadores permite la generación procedural de geometría, mientras que los constraints facilitan la animación de la cámara a lo largo de un camino definido. Este enfoque es útil para crear visualizaciones arquitectónicas, animaciones de movimiento y otros efectos visuales.

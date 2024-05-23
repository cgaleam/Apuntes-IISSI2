# Apuntes-IISSI2

Enlaces examenes
https://github.com/IISSI2-IS-2022-2023/Parciales 
https://github.com/IISSI2-IS-profs/DeliverUS-Owner-Monorepo-Enunciados-y-Soluciones

https://github.com/pablobuza014/DeliverUS-OwnerALL 
https://github.com/rafaelroodrgz?tab=repositories

Enlaces paginas utiles
https://reactnative.dev/docs/switch
https://static.enapter.com/rn/icons/material-community.html

Apuntes con información y donde encontrarla



BACKEND PASOS
Ver si existe la propiedad o hay que crearla:

Si no existe, tocamos migrations y models para añadir la propiedad(copia pega de otros)

Configuramos el frontend para que se vea coml debe aunque no funcione

Tocamos las rutas (seguramente un patch para actualizar solo una cosa): se llamara a la funcion de Controller al final, que la hacemos despues

Hacemos el controller:
En el controller hay que tocar el orden en todas las funciones donde se ordene incluyendo nuestra nueva propiedad
Si hay que ordenar se añade aqui el order[descuento, DESC]

Ejemplo para funciones de controller o validation con bucles for:
exports.promote = async function (req, res) {
  try {
    const restaurant = await Restaurant.findByPk(req.params.restaurantId) // Restaurante
    const restaurantes = await Restaurant.findAll({ // Todos los restaurantes del mismo dueño
      where: {
        userId: restaurant.userId
      }
    })
    if (!restaurant.promoted) {
      for (let i = 0; i < restaurantes.length; i++) { // Pongo a false todos los restaurantes del mismo dueño (y a true el del params)
        restaurantes[i].promote = false
        await restaurantes[i].save()
      }
      restaurant.promote = true
      await restaurant.save()
    }
    res.json(restaurant)
  } catch (err) {
    res.status(500).send(err)
  }
}

Por ultimo tocar Validation para las restricciones y MiddleWare si es necesario 



FRONTEND PASOS
Tocar endpoints añadiendo la pripiedad que usa normalmente patch con la ruta misma del routes

El resto es en screen crear lo necesario para el uso(botones, switch..)

Asegurar que se cumple la propiedad, visualizar campo: llanamos a la propiedad y con && añadimos que queremos ver cuando se cumpla. Ejemplo:
{item.promoted &&
        <TextRegular textStyle={styles.text}> ¡En promoción! </TextRegular>
        }


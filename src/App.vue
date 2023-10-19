<template>
 <div class="body">
  <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <h1 class="modal-title fs-5" id="exampleModalLabel">Carrito de compras</h1>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                        <table>
                        <thead> 
                          <tr>
                            <th>Imagen</th>
                            <th>Nombre</th>
                            <th>Precio</th>
                            <th>Cantidad</th>
                            <th>Subtotal</th>
                          </tr>
                        </thead>
                        <tbody class="produc">
                          <tr v-for="(producto, index) in carrito" :key="producto.img">
                            <td class="linea"><img class="imgCarrito" :src="producto.img" alt=""></td>
                            <td class="linea">{{ producto.nombre }}</td>
                            <td class="linea">{{ producto.precio }}</td>
                            <td class="linea">
                              <!-- <button @click="quitarUno(index)">-</button> -->
                              {{ producto.cantidad }}
                              <!-- <button @click="agregarUno(index)">+</button> -->
                            </td>
                            <td class="linea">{{ producto.cantidad * producto.precio }}</td>
                            <td class="linea"><button @click="eliminar(producto)" id="eliminar">❌</button></td>
                          </tr>
                      <tr>
                        <td class="total">Total:</td>
                        <td colspan="4"></td>
                        <td class="total">{{ calcularTotal() }}</td>
                      </tr>
                    </tbody>
                        </table>
            
                    </div>
                    <div class="modal-footer"> 
                        <button @click="vaciar()" type="button" class="btn btn-primary" id="guardar">Vaciar carrito</button>
                    </div>
                </div>
              </div>
            </div>
  <div class="pestañaFija">
    <h1 class="nombre">La Gema Dorada</h1>
    <button type="button" id="carrito" class="btn btn-primary" data-bs-toggle="modal"
                data-bs-target="#exampleModal" @click="ver()">
                <img src="https://purepng.com/public/uploads/large/purepng.com-shopping-cartshoppingcarttrolleycarriagebuggysupermarkets-1421526532688qs8ef.png" alt="2%">
            </button>

          
       
        </div>

        <div class="fondo">
          <img src="https://i.pinimg.com/originals/95/5a/8b/955a8b8c5c76d9da1c579c79aa7bc7bf.jpg" alt="">
        </div>
  <div class="titulo">
    <h2>Accesorios de Dama</h2>
  </div>
 <div class="objetos">
    <div class="obj"  v-for="(objeto, index) in data" :key="index">
      <img :src="objeto.img" alt="">
      <div class="caracter">
        <p>{{ objeto.nombre }}</p>
        <p>{{ objeto.material }}</p>
        <p>{{ objeto.talla }}</p>
        <p>{{ objeto.precio }}</p>
        <div>
          <span v-for="n in calcularEstrellas(objeto.puntuacion)" :key="n">⭐</span>
        </div>
      </div>
      <button @click="agregar(objeto)">Agregar al carrito</button>
    </div>
  </div>
 </div>

</template>

<script setup>
import { ref } from 'vue';/* 
const mostrar = ref(false); */
const carrito = ref([]);

let data=ref([
  {
    img:"https://i0.wp.com/www.dhresource.com/0x0s/f2-albu-g8-M00-75-93-rBVaVFyKK5qAD54KAAQJwrE726k204.jpg/conjuntos-de-joyas-para-mujeres-plata-925.jpg",
    nombre:"Producto 1",
    material:"Plata",
    talla:"10",
    precio:"2000.00$",
    puntuacion: 3,
  },
  {
    img:"https://i.pinimg.com/originals/db/f0/1f/dbf01f3d1e71e64f5da173b0c2126dc7.jpg",
    nombre:"Producto 2",
    material:"Plata",
    talla:"2332",
    precio:"3000.00",
    puntuacion: 5,
  },
  {
    img:"https://www.joyeriasergell.com/wp-content/uploads/2020/11/SERGELL-boton-IDEAS-REGALO-MUJER.jpg",
    nombre:"Producto 3",
    material:"Plata",
    talla:"2332",
    precio:"3000.00",
    puntuacion: 5,
  },
  {
    img:"https://m.media-amazon.com/images/I/61QFXvreddL._AC_UY625_.jpg",
    nombre:"Producto 4",
    material:"Plata",
    talla:"2332",
    precio:"2000.00",
    puntuacion: 5,
  },
  {
    img:"https://http2.mlstatic.com/estuche-de-joyas-oro-18k-plata-anillos-collar-pulsera-aretes-D_NQ_NP_845905-MPE25087170923_102016-F.jpg",
    nombre:"Producto 5",
    material:"Plata",
    talla:"2332",
    precio:"1000.00",
    puntuacion: 5,
  },
  {
    img:"https://i.pinimg.com/736x/c8/8e/6f/c88e6f3932cfc1d4a4bf068f9826a6fb.jpg",
    nombre:"Producto 6",
    material:"Oro Golfi",
    talla:"2332",
    precio:"8000.00",
    puntuacion: 5,
  },
  {
    img:"https://http2.mlstatic.com/collares-premium-dama-moda-vintage-joyeria-bisuteria-mayoreo-D_NQ_NP_800993-MLM32945108976_112019-F.jpg",
    nombre:"Producto 7",
    material:"Plata",
    talla:"2332",
    precio:"7000.00",
    puntuacion: 5,
  },
  {
    img:"https://i.pinimg.com/originals/5b/bc/49/5bbc4966037c1793f067bc4a2a81e40b.png",
    nombre:"Producto 8",
    material:"Oro Golfi",
    talla:"2332",
    precio:"6000.00",
    puntuacion: 5,
  },
  {
    img:"https://http2.mlstatic.com/juego-joyas-collar-pulsera-aretes-anillo-regalo-mujer-D_NQ_NP_791321-MPE20729008831_052016-F.jpg",
    nombre:"Producto 9",
    material:"Plata",
    talla:"2332",
    precio:"5000.00",
    puntuacion: 5,
  },
  {
    img:"https://http2.mlstatic.com/D_NQ_NP_886773-MLM45523430422_042021-F.jpg",
    nombre:"Producto 10",
    material:"Oro Golfi",
    talla:"2332",
    precio:"4000.00",
    puntuacion: 5,
  },
  {
    img:"https://mariadelao.mx/wp-content/uploads/2021/02/kit-joyeria-para-mujer-4-completo.jpg",
    nombre:"Producto 11",
    material:"Oro Golfi",
    talla:"2332",
    precio:"3000.00",
    puntuacion: 5,
  },
  {
    img:"https://i.pinimg.com/originals/09/8e/4e/098e4ea2b61733d920fe0d4a87ce8dbe.jpg",
    nombre:"Producto 12",
    material:"Oro Golfi",
    talla:"2332",
    precio:"1000.00",
    puntuacion: 5,
  }
]);

function agregarUno(index) {
  carrito.value[index].cantidad++;
}

function quitarUno(index) {
  if (carrito.value[index].cantidad > 1) {
    carrito.value[index].cantidad--;
  }
}

function eliminar(item) {
  console.log(item)
  const index = carrito.value.findIndex(cartItem => cartItem === item);
  if (index !== -1) {
    carrito.value.splice(index, 1);
  }
}

function agregar(item) {
  const carritoItem = carrito.value.find(cartItem => cartItem.img === item.img);
  if (carritoItem) {
    carritoItem.cantidad++;
  } else {
    carrito.value.push({ ...item, cantidad: 1 });
  }
}
function calcularEstrellas(puntuacion) {
  return Math.round(puntuacion);
} 

function ver(){
  console.log(carrito);
}

function calcularTotal() {
  return carrito.value.reduce((total, item) => total + item.precio * item.cantidad, 0);
}

function vaciar(){
  carrito.value = [];
}


</script>

<style scoped>
.body {
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #DAE3E5;
  font-family: Arial, sans-serif;
}

.pestañaFija {
  position: fixed;
  top:0;
  left: 0;
  width: 100%;
  background-color: #507BCD;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 20px;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
}
.nombre {
  color: #04080F;
  font-size: 50px;
  font-family:'Times New Roman', Times, serif;
  font-weight: 600;
}
img{
  width: 100%;
}
.objetos {
  margin-top: 20px;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
}

.obj {
  border: 1px solid #A1C6EA;
  padding: 10px;
  text-align: center;
  background-color: #A1C6EA;
}

.obj img {
  max-width: 100%;
}

.caracter p {
  margin: 5px 0;
  font-size: 14px;
}

.obj button {
  margin-top: 10px;
  padding: 5px 10px;
  background-color: #04080F;
  color:#DAE3E5 ;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.obj button:hover {
  background-color: #507BCD;
}
.imgCarrito{
  height: 100%;
  width: 100%;
}
.modal-body {
  padding: 20px;
  margin-left: -2%;
}

.produc td {
  padding: 10px;
  border: 2.5px solid #04080F;
  text-align: center;
  color: #04080F;
  font-family: 'Times New Roman', Times, serif;
}

.total {
  font-weight: bold;
}
#carrito{
  width: 4%;
  background-color: #507BCD;
  border: solid #04080F;
  box-shadow: #04080F 2px 2px 10px ;
}
.modal-content{
  border-radius: 0%;
  box-shadow: 2px 2px 10px #A1C6EA;
  background-color: #A1C6EA
}
h2{
  color: #04080F;
  font-family: 'Times New Roman', Times, serif;
  font-weight: 600;
}
#exampleModalLabel{
  color: #04080F;
  font-family: 'Times New Roman', Times, serif;
  font-weight: 600;
}
tr{
  color: #04080F;
  font-family: 'Times New Roman', Times, serif;
}
#guardar{
  color: #A1C6EA;
  background-color: #04080F;
  border-radius: 0%;
  box-shadow: #507BCD 2px 2px 10px;
  border:  solid transparent;
}
#eliminar{
  background-color: #04080F;
}
</style>


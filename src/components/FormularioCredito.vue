<template>
  <div class="presupuestador-menu">
    <div class="menu-progreso">
      <div class="numero" :class="{ 'numero-con-relleno': section >= 1 }">
        1
      </div>
      <div class="linea" :class="{ 'linea-con-relleno': section >= 2 }"></div>
      <div class="numero" :class="{ 'numero-con-relleno': section >= 2 }">
        2
      </div>
      <div class="linea" :class="{ 'linea-con-relleno': section >= 3 }"></div>
      <div class="numero" :class="{ 'numero-con-relleno': section >= 3 }">
        3
      </div>
      <div class="linea" :class="{ 'linea-con-relleno': section >= 4 }"></div>
      <div class="numero" :class="{ 'numero-con-relleno': section >= 4 }">
        4
      </div>
      <div class="linea" :class="{ 'linea-con-relleno': section >= 5 }"></div>
      <div class="numero" :class="{ 'numero-con-relleno': section >= 5 }">
        5
      </div>
      <div class="linea" :class="{ 'linea-con-relleno': section >= 6 }"></div>
      <div class="numero" :class="{ 'numero-con-relleno': section >= 6 }">
        6
      </div>
    </div>
    <div class="budget">
      <form @submit.prevent="submitForm">
        <div v-if="section !== 8" class="budget-form">
          <!-- Sección de contacto  -->
          <div
            v-if="section == 1 && mostrarRequisitos === true"
            class="section-requisitos"
          >
            <p>
              Si cumples con los siguientes requisitos, no dudes en solicitar tu
              crédito.
            </p>
            <p>
              a. <span>NO</span> puedes tener reportes negativos en centrales de
              riesgo.
            </p>
            <p>b. Ingresos iguales o superiores a 2.400.000</p>
            <button 
                type="button" 
                class="boton"
                @click="ocultarRequisitos">
              Continuar
            </button>
          </div>
          <div
            v-if="section == 1 && mostrarRequisitos === false"
            class="section-form"
          >
            <h2>Información de contacto</h2>
            <div>
              <div>
                <label for="nombre">Nombre:</label>
                <input
                  v-model="respuestas.nombre"
                  type="text"
                  name="et_pb_contact_first-name_0"
                  class="form-control"
                  required
                />
              </div>
              <div>
                <label for="primerApellido">Primer Apellido:</label>
                <input
                  v-model="respuestas.primerApellido"
                  type="text"
                  name="et_pb_contact_last-name_0"
                  class="form-control"
                />
              </div>
              <div>
                <label for="segundoApellido">Segundo Apellido:</label>
                <input
                  v-model="respuestas.segundoApellido"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="celular">Celular:</label>
                <input
                  :value="respuestas.celular"
                  @input="
                    $event.target.value = $event.target.value.replace(
                      /[^\d]/g,
                      ''
                    );
                    respuestas.celular = $event.target.value;
                  "
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="correoElectronico">Correo electronico:</label>
                <input
                  v-model="respuestas.correoElectronico"
                  type="text"
                  name="et_pb_contact_email_0"
                  class="form-control"
                />
              </div>
              <div>
                <label>Descripción de actividad:</label>
                <select
                  v-model="descripcionActividad"
                  class="form-select"
                  aria-label="Default select example"
                >
                  <option value="empleado">Empleado</option>
                  <option value="independiente">Independiente</option>
                  <option value="prestadorServicios">
                    Prestador de servicios
                  </option>
                </select>
              </div>
            </div>
          </div>
          <!-- Sección de información de vehiculo -->
          <div v-if="section == 2" class="section-form">
            <h2>Información del vehiculo</h2>
            <div>
              <div>
                <label for="marca">Marca:</label>
                <input
                  placeholder="Chevrolet"
                  v-model="respuestas.marca"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="linea">Línea:</label>
                <input
                  placeholder="Spark GT"
                  v-model="respuestas.linea"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="modelo">Modelo:</label>
                <input
                  placeholder="2018"
                  :value="respuestas.modelo"
                  @input="
                    $event.target.value = $event.target.value.replace(
                      /[^\d]/g,
                      ''
                    );
                    respuestas.modelo = $event.target.value;
                  "
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="valorVehiculo">Valor del vehículo:</label>
                <input
                  :value="respuestas.valorVehiculo"
                  @input="
                    $event.target.value = $event.target.value
                      .replace(/[^\d]/g, '')
                      .replace(/\B(?=(\d{3})+(?!\d))/g, '.');
                    respuestas.valorVehiculo = $event.target.value;
                  "
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="cuotaInicial">Cuota inicial:</label>
                <input
                  :value="respuestas.cuotaInicial"
                  @input="
                    $event.target.value = $event.target.value
                      .replace(/[^\d]/g, '')
                      .replace(/\B(?=(\d{3})+(?!\d))/g, '.');
                    respuestas.cuotaInicial = $event.target.value;
                  "
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="montoFinanciar">Monto a financiar:</label>
                <input
                  :value="respuestas.montoFinanciar"
                  @input="
                    $event.target.value = $event.target.value
                      .replace(/[^\d]/g, '')
                      .replace(/\B(?=(\d{3})+(?!\d))/g, '.');
                    respuestas.montoFinanciar = $event.target.value;
                  "
                  type="text"
                  class="form-control"
                />
              </div>
            </div>
          </div>

          <!-- Sección de Información personal -->
          <div v-if="section == 3" class="section-form">
            <h2>Información personal</h2>
            <div>
              <div>
                <label>Tipo de identificación:</label>
                <select
                  v-model="respuestas.tipoIdentificacion"
                  class="form-select"
                >
                  <option value="cc">Cédula</option>
                  <option value="ce">Cédula extrajeria</option>
                </select>
              </div>
              <div>
                <label for="numeroIdentificacion"
                  >Número de identificacion:</label
                >
                <input
                  v-model="respuestas.numeroIdentificacion"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="fechaNacimiento">Fecha de nacimiento:</label>
                <input
                  placeholder="DD/MM/AÑO"
                  v-model="respuestas.fechaNacimiento"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label>Estado civil:</label>
                <select v-model="respuestas.estadoCivil" class="form-select">
                  <option value="soltero">Soltero</option>
                  <option value="casado">Casado</option>
                  <option value="viudo">Viudo</option>
                  <option value="separado">Separado</option>
                  <option value="unionLibre">U. Libre</option>
                </select>
              </div>
              <div>
                <label>Sexo:</label>
                <select v-model="respuestas.sexo" class="form-select">
                  <option value="femenino">Femenino</option>
                  <option value="masculimo">Masculino</option>
                </select>
              </div>
              <div>
                <label>Estudios realizados:</label>
                <select v-model="respuestas.estudios" class="form-select">
                  <option value="primaria">Primaria</option>
                  <option value="bachiller">Bachiller</option>
                  <option value="universitario">Universitario</option>
                  <option value="tecnologico">Tecnológico</option>
                  <option value="posgrado">Posgrado</option>
                </select>
              </div>
              <div>
                <label for="ocupacion">Ocupación u oficio:</label>
                <input
                  v-model="respuestas.ocupacion"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="profesion">Profesión:</label>
                <input
                  v-model="respuestas.profesion"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="telefono">Teléfono residencia:</label>
                <input
                  v-model="respuestas.telefono"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label
                  >Eres una persona de reconocimiento público o político:</label
                >
                <select v-model="respuestas.reconocimiento" class="form-select">
                  <option value="si">Si</option>
                  <option value="no">No</option>
                </select>
              </div>
              <div>
                <label>Tipo de vivienda:</label>
                <select v-model="respuestas.tipoVivienda" class="form-select">
                  <option value="conHipoteca">Propia con hipoteca</option>
                  <option value="sinHipoteca">Propia sin hipoteca</option>
                  <option value="arrendada">Arrendada</option>
                  <option value="familiar">Familiar</option>
                </select>
              </div>
              <div>
                <label for="direccionResidencia"
                  >Dirección de residencia:</label
                >
                <input
                  v-model="respuestas.direccionResidencia"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="ciudad">Ciudad</label>
                <input
                  v-model="respuestas.ciudad"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="barrio">Barrio:</label>
                <input
                  v-model="respuestas.barrio"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="estrato">Estrato:</label>
                <input
                  v-model="respuestas.estrato"
                  type="text"
                  class="form-control"
                />
              </div>
            </div>
          </div>
          <!-- Sección actividad laboral -->
          <div v-if="section == 4" class="section-form">
            <h2>Actividad laboral</h2>
            <div
              v-if="
                descripcionActividad === 'empleado' ||
                descripcionActividad === 'prestadorServicios'
              "
            >
              <div>
                <label for="empresa">Empresa:</label>
                <input
                  v-model="respuestas.empresa"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="cargoActual">Cargo actual:</label>
                <input
                  v-model="respuestas.cargoActual"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="fechaIngreso">Fecha de ingreso:</label>
                <input
                  placeholder="DD/MM/AÑO"
                  v-model="respuestas.fechaIngreso"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label>Tipo de contrato:</label>
                <select v-model="respuestas.tipoContrato" class="form-select">
                  <option value="terminoIndefinido">Término indefinido</option>
                  <option value="fijo">Fijo</option>
                  <option value="prestacionServicios">
                    Prestación de servicios
                  </option>
                  <option value="otro">Otro</option>
                </select>
              </div>
              <div>
                <label for="direccionEmpresa">Dirección:</label>
                <input
                  v-model="respuestas.direccionEmpresa"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="telefonoEmpresa">Teléfono:</label>
                <input
                  v-model="respuestas.telefonoEmpresa"
                  type="text"
                  class="form-control"
                />
              </div>
              <div>
                <label for="ciudadEmpresa">Ciudad:</label>
                <input
                  v-model="respuestas.ciudadEmpresa"
                  type="text"
                  class="form-control"
                />
              </div>
            </div>
            <div v-if="descripcionActividad === 'independiente'">
              <div>
                <label>Actividad económica:</label>
                <select
                  v-model="respuestas.actividadEconomica"
                  class="form-select"
                >
                  <option value="comerciante">Comerciante</option>
                  <option value="empresario">Empresario</option>
                  <option value="transportador">Transportador</option>
                  <option value="rentistaCapital">Rentista de capital</option>
                  <option value="otro">Otro</option>
                </select>
              </div>
              <div>
                <label for="tiempoActividad">Tiempo en actividad:</label>
                <input
                  placeholder="Dos años"
                  v-model="respuestas.tiempoActividad"
                  type="text"
                  class="form-control"
                />
              </div>

            </div>
          </div>

          <!-- Sección de Relación ingresos y egresos-->
          <div v-if="section == 5">
            <h2>Relación ingresos y egresos</h2>
            <div class="section-form__ingresos">
              <div>
                <h3>Ingresos mensuales</h3>
                <div class="grupo-ingresos">
                  <div>
                    <label for="salario">Salario:</label>
                    <input
                      :value="respuestas.salario"
                      @input="
                        $event.target.value = $event.target.value
                          .replace(/[^\d]/g, '')
                          .replace(/\B(?=(\d{3})+(?!\d))/g, '.');
                        respuestas.salario = $event.target.value;
                      "
                      type="text"
                      class="form-control"
                    />
                  </div>
                  <div class="grupo-ingresos_honorarios">
                    <label for="honorarios">Honorarios:</label>
                    <input
                      :value="respuestas.honorarios"
                      @input="
                        $event.target.value = $event.target.value
                          .replace(/[^\d]/g, '')
                          .replace(/\B(?=(\d{3})+(?!\d))/g, '.');
                        respuestas.honorarios = $event.target.value;
                      "
                      type="text"
                      class="form-control"
                    />
                  </div>
                  <div>
                    <label for="otrosIngresos">Otros:</label>
                    <input
                      :value="respuestas.otrosIngresos"
                      @input="
                        $event.target.value = $event.target.value
                          .replace(/[^\d]/g, '')
                          .replace(/\B(?=(\d{3})+(?!\d))/g, '.');
                        respuestas.otrosIngresos = $event.target.value;
                      "
                      type="text"
                      class="form-control"
                    />
                  </div>
                </div>
              </div>
            </div>
            <div>
              <div class="section-form__egresos">
                <h3>Egresos mensuales:</h3>
                <div>
                  <div class="grupo-OtrosGastos">
                    
                    <div class="grupo-OtrosGastos_familiares">
                      <label for="gastosFamiliares">Gastos familiares:</label>
                      <input
                        :value="respuestas.gastosFamiliares"
                        @input="
                          $event.target.value = $event.target.value
                            .replace(/[^\d]/g, '')
                            .replace(/\B(?=(\d{3})+(?!\d))/g, '.');
                          respuestas.gastosFamiliares = $event.target.value;
                        "
                        type="text"
                        class="form-control"
                      />
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Sección de Referencias -->
          <div v-if="section == 6">
            <div v-if="!submit">
            <h2>Referencias</h2>
            <div>
              <div>
                <h3>Referencias familiares:</h3>
                <div class="section-form__referencias">
                  <div class="section-form__referencia">
                    <div>
                      <label for="nomvbre">Nombre</label>
                      <input
                        v-model="respuestas.referenciaFamiliar1.nombre"
                        type="text"
                        class="form-control"
                      />
                    </div>
                    <div>
                      <label for="telefono">Celular:</label>
                      <input
                        v-model="respuestas.referenciaFamiliar1.celular"
                        type="text"
                        class="form-control"
                      />
                    </div>
                    <div>
                      <label for="ciudad">Ciudad:</label>
                      <input
                        v-model="respuestas.referenciaFamiliar1.ciudad"
                        type="text"
                        class="form-control"
                      />
                    </div>
                  </div>
                  <div class="section-form__referencia">
                    <div>
                      <label for="nomvbre">Nombre</label>
                      <input
                        v-model="respuestas.referenciaFamiliar2.nombre"
                        type="text"
                        class="form-control"
                      />
                    </div>
                    <div>
                      <label for="telefono">Celular:</label>
                      <input
                        v-model="respuestas.referenciaFamiliar2.celular"
                        type="text"
                        class="form-control"
                      />
                    </div>
                    <div>
                      <label for="ciudad">Ciudad:</label>
                      <input
                        v-model="respuestas.referenciaFamiliar2.ciudad"
                        type="text"
                        class="form-control"
                      />
                    </div>
                  </div>
                </div>
                <div class="section-form__referencias">
                  <h3>Referencias personales:</h3>
                  <div class="section-form__referencia">
                    <div>
                      <label for="nomvbre">Nombre</label>
                      <input
                        v-model="respuestas.referenciaPersonal1.nombre"
                        type="text"
                        class="form-control"
                      />
                    </div>
                    <div>
                      <label for="telefono">Celular:</label>
                      <input
                        v-model="respuestas.referenciaPersonal1.celular"
                        type="text"
                        class="form-control"
                      />
                    </div>
                    <div>
                      <label for="ciudad">Ciudad:</label>
                      <input
                        v-model="respuestas.referenciaPersonal1.ciudad"
                        type="text"
                        class="form-control"
                      />
                    </div>
                  </div>
                  <div class="section-form__referencia">
                    <div>
                      <label for="nomvbre">Nombre</label>
                      <input
                        v-model="respuestas.referenciaPersonal2.nombre"
                        type="text"
                        class="form-control"
                      />
                    </div>
                    <div>
                      <label for="telefono">Celular:</label>
                      <input
                        v-model="respuestas.referenciaPersonal2.celular"
                        type="text"
                        class="form-control"
                      />
                    </div>
                    <div>
                      <label for="ciudad">Ciudad:</label>
                      <input
                        v-model="respuestas.referenciaPersonal2.ciudad"
                        type="text"
                        class="form-control"
                      />
                    </div>
                  </div>
                </div>
                <div
                  v-if="
                    descripcionActividad === 'independiente' ||
                    descripcionActividad === 'prestadorServicios'
                  "
                  class="section-form__referencias"
                >
                  <h3>Referencias comerciales:</h3>
                  <div class="section-form__referencia">
                    <div>
                      <label for="nomvbre">Nombre</label>
                      <input
                        v-model="respuestas.referenciaComercial1.nombre"
                        type="text"
                        class="form-control"
                      />
                    </div>
                    <div>
                      <label for="telefono">Celular:</label>
                      <input
                        v-model="respuestas.referenciaComercial1.celular"
                        type="text"
                        class="form-control"
                      />
                    </div>
                    <div>
                      <label for="ciudad">Ciudad:</label>
                      <input
                        v-model="respuestas.referenciaComercial1.ciudad"
                        type="text"
                        class="form-control"
                      />
                    </div>
                    <div>
                      <label for="cedula">Cédula o Nit:</label>
                      <input
                        v-model="respuestas.referenciaComercial1.cedula"
                        type="text"
                        class="form-control"
                      />
                    </div>
                  </div>
                  <div class="section-form__referencia">
                    <div>
                      <label for="nomvbre">Nombre</label>
                      <input
                        v-model="respuestas.referenciaComercial2.nombre"
                        type="text"
                        class="form-control"
                      />
                    </div>
                    <div>
                      <label for="telefono">Celular:</label>
                      <input
                        v-model="respuestas.referenciaComercial2.celular"
                        type="text"
                        class="form-control"
                      />
                    </div>
                    <div>
                      <label for="ciudad">Ciudad:</label>
                      <input
                        v-model="respuestas.referenciaComercial2.ciudad"
                        type="text"
                        class="form-control"
                      />
                    </div>
                    <div>
                      <label for="cedula">Cédula o Nit:</label>
                      <input
                        v-model="respuestas.referenciaComercial2.cedula"
                        type="text"
                        class="form-control"
                      />
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div>
              <label style="margin-right: 8px;">Firma: </label>
              <canvas
                ref="canvas"
                :width="canvasWidth"
                :height="canvasHeight"
                style="border: 1px solid #ced4da;"
              ></canvas>
              <div>
              <button
                type="button"
                class="boton"
                @click.prevent.stop="limpiarFirma"
              >
                Limpiar Firma
              </button>
              </div>
            </div>
            </div>
            <div class="contactar" v-if="submitComplete">
              <p>Estás a un paso de cumplir con tu proyecto de vehículo</p>
              <p>Para iniciar el proceso de crédito envia una foto de tu cédula {{ descripcionActividad === 'independiente' ? 'y RUT a tu asesor por WhatsApp' : 'a tu asesor por WhatsApp' }} </p>
              <div><button @click="contactarAsesor" class="boton" type="button">Contactar asesor</button></div>
            </div>
          </div>
        </div>
        <div v-if="!submit" class="contenedor-botones">
          <button
            type="button"
            class="boton"
            :class="widthAnterior"
            @click="anterior"
            v-if="section !== 1"
          >
            Anterior
          </button>
          <button
            type="button"
            @click="proximo"
            :class="disabledButton ? 'boton-desabilitado' : !disabledButton && section === 1 ? 'boton envio-registro' : 'boton'" :disabled="disabledButton"
            v-if="section !== 6 && mostrarRequisitos === false"
          >
            Próximo
          </button>
        </div>
        <div v-if="!submit" class="boton-enviar">
          <button :class="disabledButton ? 'submit-desabilitado' : 'submit'" :disabled="disabledButton" v-if="section == 6" type="submit">Enviar</button>
        </div>
      </form>
    </div>
    <!-- Ruleta de carga -->
    <div v-if="loading" class="loading-spinner">
      <div class="spinner"></div>
    </div>
  </div>
</template>

<script>
import { PDFDocument } from "pdf-lib";
import { initializeApp } from "firebase/app";
import { getFirestore } from "firebase/firestore";
import { collection, addDoc } from "firebase/firestore";
import { getStorage, ref, uploadBytes } from "firebase/storage";

const firebaseConfig = {
  apiKey: "AIzaSyCX6kqJyaW8d7jmAmomWNkKFEjSTEboIDg",
  authDomain: "pdf-credito-d72e6.firebaseapp.com",
  projectId: "pdf-credito-d72e6",
  storageBucket: "pdf-credito-d72e6.appspot.com",
  messagingSenderId: "13266000813",
  appId: "1:13266000813:web:f4e878c57d4e571fad1f24",
  measurementId: "G-56F8P4D7QM",
};

export default {
  data() {
    return {
      submit:false,
      loading: false,
      submitComplete: false,
      mostrarRequisitos: true,
      section: 1,
      descripcionActividad: "empleado",
      respuestas: {
        nombre: "",
        primerApellido: "",
        segundoApellido: "",
        celular: "",
        correoElectronico: "",
        marca: "",
        linea: "",
        modelo: "",
        valorVehiculo: "",
        cuotaInicial: "",
        montoFinanciar: "",
        tipoIdentificacion: "cc",
        numeroIdentificacion: "",
        fechaNacimiento: "",
        estadoCivil: "soltero",
        sexo: "femenino",
        estudios: "universitario",
        ocupacion: "",
        profesion: "",
        telefono: "",
        reconocimiento: "no",
        tipoVivienda: "arrendada",
        direccionResidencia: "",
        ciudad: "",
        barrio: "",
        estrato: "",
        empresa: "",
        cargoActual: "",
        fechaIngreso: "",
        tipoContrato: "",
        direccionEmpresa: "",
        telefonoEmpresa: "",
        ciudadEmpresa: "",
        actividadEconomica: "",
        tiempoActividad: "",
        salario: "",
        honorarios: "",
        otrosIngresos: "",
        gastosFamiliares: "",
        referenciaFamiliar1: {
          nombre: "",
          celular: "",
          ciudad: "",
        },
        referenciaFamiliar2: {
          nombre: "",
          celular: "",
          ciudad: "",
        },
        referenciaPersonal1: {
          nombre: "",
          celular: "",
          ciudad: "",
        },
        referenciaPersonal2: {
          nombre: "",
          celular: "",
          ciudad: "",
        },
        referenciaComercial1: {
          nombre: "",
          celular: "",
          ciudad: "",
          cedula: "",
        },
        referenciaComercial2: {
          nombre: "",
          celular: "",
          ciudad: "",
          cedula: "",
        },
      },
      firma: null,
      canvasWidth: 280,
      canvasHeight: 100,
      pdfBytes: null,
    };
  },
  watch: {
    section(value) {
      if (value === 6) {
        this.$nextTick(() => {
          this.inicializarCanvas();
        });
      }
      window.scrollTo(0, 0);
    }    
  },
  computed: {
    disabledButton() {
      if (this.section === 1) {
        return !(
          this.respuestas.nombre &&
          this.respuestas.primerApellido &&
          this.respuestas.celular &&
          this.respuestas.correoElectronico
        );
      } else if (this.section === 2) {
        return !(
          this.respuestas.marca &&
          this.respuestas.modelo &&
          this.respuestas.montoFinanciar
        );
      } else if (this.section === 3) {
        return !(
          this.respuestas.numeroIdentificacion &&
          this.respuestas.fechaNacimiento &&
          this.respuestas.ocupacion &&
          this.respuestas.direccionResidencia &&
          this.respuestas.ciudad &&
          this.respuestas.barrio
        );
      } else if (
        this.section === 4 &&
        (this.descripcionActividad === "empleado" ||
          this.descripcionActividad === "prestadorServicios")
      ) {
        return !(
          this.respuestas.empresa &&
          this.respuestas.cargoActual &&
          this.respuestas.fechaIngreso &&
          this.respuestas.tipoContrato &&
          this.respuestas.telefonoEmpresa &&
          this.respuestas.ciudadEmpresa
        );
      } else if (
        this.section === 4 &&
        this.descripcionActividad === "independiente"
      ) {
        return !(
          this.respuestas.actividadEconomica && this.respuestas.tiempoActividad
        );
      } else if (this.section === 5) {
        return !(this.respuestas.salario || this.respuestas.honorarios);
      } else if (this.section === 6) {
        return !this.firma;
      } else {
        // Valor de retorno predeterminado
        return true;
      }
    },
    widthAnterior(){
      if(this.section === 6){
         return { widthBoton:true};
      }else{
        return { boton:true};
      }
    }
  },
  methods: {
     inicializarCanvas() {
      const canvas = this.$refs.canvas;
      const ctx = canvas.getContext("2d");
      ctx.fillStyle = "white";
      ctx.fillRect(0, 0, this.canvasWidth, this.canvasHeight);

      let dibujando = false;
      let lastX = 0;
      let lastY = 0;

      const dibujar = (x, y) => {
        if (!dibujando) return;
        ctx.beginPath();
        ctx.moveTo(lastX, lastY);
        ctx.lineTo(x, y);
        ctx.strokeStyle = "black";
        ctx.lineWidth = 2;
        ctx.stroke();
        [lastX, lastY] = [x, y];
      };

      const iniciarDibujo = (x, y) => {
        dibujando = true;
        [lastX, lastY] = [x, y];
      };

      const finalizarDibujo = () => {
        dibujando = false;
        this.guardarFirma();
      };

      // Eventos para el mouse
      canvas.addEventListener("mousedown", (e) => iniciarDibujo(e.offsetX, e.offsetY));
      canvas.addEventListener("mousemove", (e) => dibujar(e.offsetX, e.offsetY));
      canvas.addEventListener("mouseup", finalizarDibujo);
      canvas.addEventListener("mouseout", finalizarDibujo);

      // Eventos para dispositivos táctiles
      canvas.addEventListener("touchstart", (e) => {
        const touch = e.touches[0];
        const rect = canvas.getBoundingClientRect();
        iniciarDibujo(touch.clientX - rect.left, touch.clientY - rect.top);
      });

      canvas.addEventListener("touchmove", (e) => {
        e.preventDefault(); // Prevenir el desplazamiento de la página al dibujar
        const touch = e.touches[0];
        const rect = canvas.getBoundingClientRect();
        dibujar(touch.clientX - rect.left, touch.clientY - rect.top);
      });

      canvas.addEventListener("touchend", finalizarDibujo);
      canvas.addEventListener("touchcancel", finalizarDibujo);
    },
    ocultarRequisitos() {
      this.mostrarRequisitos = false;
      
    },
    ocultarBoton() {
      this.mostrarBoton = false;
    },
    anterior() {
      // Lógica para la acción del botón "Anterior"
      this.section -= 1;
    },
    proximo() {
      // Lógica para la acción del botón "Próximo"
      if (this.section === 1) {
        this.guardarRegistro();
        window.dataLayer = window.dataLayer || [];
        window.dataLayer.push({
        event: "registro_enviado"
      });
      }

      this.section += 1;
    },
    limpiarFirma() {
      const canvas = this.$refs.canvas;
      const ctx = canvas.getContext("2d");
      ctx.clearRect(0, 0, this.canvasWidth, this.canvasHeight);
      this.firma = null;
    },
    guardarFirma() {
      const canvas = this.$refs.canvas;
      this.firma = canvas.toDataURL();
    },
    async rellenarPDF() {
      // Cargar el PDF existente
      const urlPDF =
        "https://abba-ahorro-inversion.s3.us-east-2.amazonaws.com/Versi%C3%B3n+actualizada+Final";
      const existingPDFBytes = await fetch(urlPDF).then((res) =>
        res.arrayBuffer()
      );

      // Crear un nuevo documento PDF
      const pdfDoc = await PDFDocument.load(existingPDFBytes);
      const form = pdfDoc.getForm();
      const imageBytes = Uint8Array.from(atob(this.firma.split(",")[1]), (c) =>
        c.charCodeAt(0)
      );
      //const fields = form.getFields();

      // Conectar respuestas del formulario con campos del PDF
      const fieldNames = [
        "Nombre",
        "1 Apellido",
        "2 Apellido",
        "Celular",
        "Correo Electronico",
        "Marca",
        "Linea",
        "Modelo",
        "Valor Comercial",
        "Cuaota Inicial",
        "Monto Financiar",
        `${
          this.respuestas.tipoIdentificacion === "cc"
            ? "untitled82"
            : "untitled83"
        }`,
        "Numero",
        "Fecha Nacimiento",
        `${
          this.respuestas.estadoCivil === "soltero"
            ? "untitled91"
            : this.respuestas.estadoCivil === "casado"
            ? "untitled90"
            : this.respuestas.estadoCivil === "separado"
            ? "untitled89"
            : this.respuestas.estadoCivil === "viudo"
            ? "untitled88"
            : "untitled87"
        }`,
        `${
          this.respuestas.sexo === "femenino" ? "untitled92" : "untitled93"
        }`,
        `${
          this.respuestas.estudios === "primaria"
            ? "untitled94"
            : this.respuestas.estudios === "bachiller"
            ? "untitled95"
            : this.respuestas.estudios === "universitario"
            ? "untitled96"
            : this.respuestas.estudios === "tecnologico"
            ? "untitled97"
            : "untitled98"
        }`,
        "Ocupación u oficio",
        "Profesión",
        "Telefono residencia",
        `${
          this.respuestas.reconocimiento === "si"
            ? "untitled102"
            : "untitled103"
        }`,
       `${
          this.respuestas.tipoVivienda === "conHipoteca"
            ? "untitled104"
            : this.respuestas.tipoVivienda === "sinHipoteca"
            ? "untitled105"
            : this.respuestas.tipoVivienda === "arrendada"
            ? "untitled106"
            : "untitled107"
        }`,
        "Direcciòn Residencia",
        "Ciudad",
        "Barrio",
        "Estrato",
        "Empresa",
        "Cargo Actual",
        "Fecha de ingreso",
        `${
          this.respuestas.tipoContrato === "terminoIndefinido"
            ? "untitled108"
            : this.respuestas.tipoContrato === "fijo"
            ? "untitled109"
            : this.respuestas.tipoContrato === "prestacionServicios"
            ? "untitled110"
            : "untitled111"
        }`,
        "Direcciòn Principal",
        "Telefono",
        "Ciudad",
         `${
          this.respuestas.actividadEconomica === "comerciante"
            ? "untitled112"
            : this.respuestas.actividadEconomica === "empresario"
            ? "untitled113"
            : this.respuestas.actividadEconomica === "transportador"
            ? "untitled114"
            : this.respuestas.actividadEconomica === "rentistaCapital"
            ? "untitled115"
            : "untitled116"
        }`,
        "Tiempo de actividad",
        "Salario",
        "Honorarios",
        "Otros Ingresos",
        "Gastos Familiares",
        "Nombre Familiar 1",
        "Telefono 1",
        "Ciudad 1",
        "Nombre Familiar 2",
        "Telefono 2",
        "Ciudad 2",
        "Nombre Familiar 3",
        "Telefono 3",
        "Ciudad 3",
        "Nombre Familiar 4",
        "Telefono 4",
        "Ciudad 4",
        "Nombre 5",
        "Telefono 5",
        "Ciudad 5",
        "Cedula o Nit 1",
        "Nombre 6",
        "Telefono 6",
        "Ciudad 6",
        "Cedula o Nit 2"
      ]; // Identificadores únicos de los campos del PDF
      const fieldValues = Object.values(this.respuestas).flatMap((value) => {
        if (typeof value === "object") {
          return Object.values(value);
        }
        return value;
      });

      // Editar el PDF con las respuestas del formulario

      for (let i = 0; i < fieldNames.length; i++) {
        const fieldName = fieldNames[i];
        if (fieldName.includes("untitled") === true) {
          const checkBoxField = form.getCheckBox(fieldName);
          checkBoxField.check();
        } else {
          const fieldValue = fieldValues[i];
          const textField = form.getTextField(fieldName);
          textField.setText(fieldValue);
        }
      }

      const signatureImage = await pdfDoc.embedPng(imageBytes);
      const pages = pdfDoc.getPages();
      const thirdPage = pages[2];
      const { width, height } = thirdPage.getSize();
      const imageWidth = signatureImage.width;
      const imageHeight = signatureImage.height;
      const x = width - imageWidth - 85; // Ajustar 50 según sea necesario
      const y = height - imageWidth - 290; // Ajustar según sea necesario

      // Dibujar la imagen de la firma en la tercera página
      thirdPage.drawImage(signatureImage, {
        x: x,
        y: y,
        width: imageWidth,
        height: imageHeight,
      });

      // Guardar el PDF modificado
      const pdfBytes = await pdfDoc.save();
      return pdfBytes;
    },
    async guardarRegistro() {
      const firebaseApp = initializeApp(firebaseConfig);
      const db = getFirestore(firebaseApp);

       const colección = collection(db, "registros");
       const nuevoDocumento = await addDoc(colección, {
        name: `${this.respuestas.nombre} ${this.respuestas.primerApellido}`,
        email: this.respuestas.correoElectronico,
        celular: this.respuestas.celular,
      });

       console.log(nuevoDocumento);
     },
    async guardarPDFFirestore(pdfBytes) {
      try {
        const app = initializeApp(firebaseConfig);
        const storage = getStorage(app);

        // Guardar el PDF en Firestore
        const fileName = `pdf_${new Date().getTime()}.pdf`;

        // Crear una referencia al archivo en Firebase Storage
        const storageRef = ref(storage, fileName);

        // Subir los bytes del PDF al almacenamiento
        await uploadBytes(storageRef, pdfBytes);

        // console.log('PDF almacenado en Firestore con ID:');
      } catch (error) {
        console.error("Error al almacenar el PDF en Firestore:", error);
      }
    },
    async submitForm() {
      this.loading = true; 
      this.submit = true;
      try {
        // Rellenar el PDF con las respuestas
        this.pdfBytes = await this.rellenarPDF();
        await this.guardarPDFFirestore(this.pdfBytes);
         this.submitComplete = true;
      } catch (error) {
        console.error("Error al rellenar el PDF:", error);
      } finally {
        this.loading = false;  // Ocultar la ruleta de carga
      }
    },
    contactarAsesor(){
       window.location.href="https://wa.link/hxop5c"
    }
  }
}
</script>

<style scoped>
.presupuestador-menu {
  position: relative;
  max-width: 100%;
  padding: 1.25rem;
  color: #333333;
  margin-top: 0;
}

input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
}

.backdrop {
  height: 100%;
  width: 100%;
  opacity: 0.7;
  /*background-color: rgba(0, 0, 0, 0.75);*/
  z-index: 10;
}

.loading-spinner {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 1000;
}

.spinner {
  border: 8px solid rgba(0, 0, 0, 0.1);
  border-top: 8px solid #3498db;
  border-radius: 50%;
  width: 60px;
  height: 60px;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

form {
  width: 100%;
}

.menu-progreso {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0;
}

.numero {
  width: 35px;
  height: 35px;
  border: 3px solid #ddd;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: bold;
  margin: 0;
  position: relative;
}

.numero-con-relleno {
  border: #3498db;
  background-color: #3498db;
  color: #fff;
}

.linea {
  flex: 1;
  height: 5px;
  background-color: #ddd;
  margin: 0;
  z-index: -1;
}

.linea-con-relleno {
  background-color: #3498db;
}

.budget {
  display: flex;
  flex-direction: column;
}

.section-requisitos {
  margin-top: 2rem;
}

.section-requisitos span {
  font-weight: bold;
}

.section-form div {
  display: grid;
}

h2 {
  font-size: 28px;
  text-align: center;
  margin: 30px 0;
}

h3 {
  font-size: 24px;
  margin-bottom: 13px;
}

label {
  font-weight: bold;
  color: #555555;
  margin: 0 0 4px;
}

input,
select {
  margin: 0 0 15px;
  /*padding: 1px 0 1px 9px;*/
}

::placeholder {
  color: #e0dede;
}

.section-form select {
  padding: 6px 12px;
  border: 1px solid #ced4da;
  height: 38px;
  /*padding: 1px 0 1px 9px;*/
}
.contenedor-botones {
  display: flex;
}

.boton {
  /*padding: 10px 20px;*/
  padding: 11px;
  /*margin: 0 10px;*/
  margin: 15px 0;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 5px;
  outline: none;
}

.widthBoton {
    width:127.81px;
}

.boton-enviar{
  display: grid;
  justify-content: center;
  margin: 15px 0;
}

.submit{
    all: unset;
    font-family: Helvetica, Arial, sans-serif;
    display: inline-block;
    max-width: 100%;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    background-color: #f08935;
    color: #fff;
    font-size: 18px;
    border-radius: 5px;
    padding: 0 30px;
    font-weight: bold;
    height: 45px;
    cursor: pointer;
    line-height: 45px;
    text-align: center;
   /*margin: 15px 0;*/
    text-decoration: none;
}

.submit:hover {
  background-color: #f58021;
}

.submit-desabilitado {
  all: unset;
    font-family: Helvetica, Arial, sans-serif;
    display: inline-block;
    max-width: 100%;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    background-color: #6c757d;
    border-color: #6c757d;
   border: none;
    color: #fff;
    font-size: 18px;
    border-radius: 5px;
    padding: 0 30px;
    font-weight: bold;
    height: 45px;
    cursor: pointer;
    line-height: 45px;
    text-align: center;
   /*margin: 15px 0;*/
    text-decoration: none;
     outline: none;
    opacity: 0.65;
}

.boton-desabilitado {
  margin: 15px 0;
  font-size: 18px;
  padding: 11px;
  color: #fff;
  background-color: #6c757d;
  border-color: #6c757d;
  border: none;
  border-radius: 5px;
  outline: none;
  opacity: 0.65;
}
.contenedor-botones button:nth-child(1) {
  margin-left: 0;
  margin-right: 30px;
}

.boton:hover {
  background-color: #2980b9;
}

.section-form__egresos h3 {
  margin-bottom: 13px;
}

.section-form__egreso {
  display: grid;
  grid-template-columns: 45% 45%;
  margin-bottom: 12px;
  align-items: center;
}

/*.section-form__ingresos div:nth-child(1) {
  display: grid;
  align-items: center;
}

.section-form__ingresos div:nth-child(2) {
  display: flex;
  flex-direction: column;
}*/

.section-form__referencias {
  display: grid;

}

.section-form__referencia {
  display: flex;
  flex-wrap: wrap;
}

.section-form__referencia div {
   margin-right: 12px;
   width: 100%;
}

.contactar{
   margin-top: 2.5rem;
   font-size: 18px;
  color: #000000;
  font-family: 'Open Sans';

}

@media (min-width: 22.5rem) {
  .section-form__referencia div {
   width: 45%;
}
}

@media (min-width: 31.25rem) {
  .presupuestador-menu {
    padding: 2.5rem;
  }
}

@media (min-width: 37.5rem) {
  .grupo-OtrosGastos {
    display: grid;
    grid-template-columns: 44% 46%;
  }

  .grupo-OtrosGastos_familiares {
    /* margin-left: 10px; */
  }

  .section-form__referencia div {
   width: 30%;
}
}

@media (min-width: 49.1rem) {
  .presupuestador-menu {
    border-radius: 12px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    margin: 1.25rem;
  }

  .budget {
    flex-direction: row;
  }

  form {
    order: 2;
    padding-left: 40px;
  }
}

@media (min-width: 62.5rem) {
  .presupuestador-menu {
    margin: 2rem;
  }

  .section-form div {
    display: grid;
    grid-template-columns: 45% 45%;
  }

  .section-form label {
    margin-right: 10px;
  }

  .section-form input {
    margin-right: 10px;
  }

  .grupo-ingresos {
    display: grid;
    grid-template-columns: 45% 45%;
  }

  .grupo-ingresos_honorarios {
    margin-left: 10px;
  }
}
</style>
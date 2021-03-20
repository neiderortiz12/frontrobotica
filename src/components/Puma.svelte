<script>
    let resource = 'estructura'
    
    let x = 15
    let y = 0
    let z = 10
    let alpha = 180
    let beta = -90
    let phi = 0

    let theta1 =0
    let theta2 =0
    let theta3 =0
    let theta4 =0
    let theta5 =0
    let theta6 =0
    let a2=5
    let d1=10
    let d4=5
    let d6=5
    let dato_dir ={
        "posicion":{
            "x":0,
            "y":0,
            "z":0
        },
        "orientacion_zyz":{
            "alpha":0,
            "beta":0,
            "phi":0
        },
        "orientacion_rpy":{
            "roll":0,
            "pitch":0,
            "yaw":0
        } 
    }
    let dato_inv ={
        "angulos":{
            "theta1":0,
            "theta2":0,
            "theta3":0,
            "theta4":0,
            "theta5":0,
            "theta6":0,
            },
        "orientacion_zyz":{
            "alpha_z":0,
            "beta_y" :0,
            "phi_z"  :0,

        }
    }
    
    function cambiarRecurso(recurso){
        resource=recurso
    }

    function directaPuma(){
        fetch('http://localhost:5001/directa', {
            method:'POST',
            body: JSON.stringify({
                robot:'puma',
                datos:{
                    d1:d1,
                    d4:d4,
                    a2:a2,
                    d6:d6,
                    theta1:theta1,
                    theta2:theta2,
                    theta3:theta3,
                    theta4:theta4,
                    theta5:theta5,
                    theta6:theta6,
                    
                }
            })
        }).then((res) =>{
            res.json().then((datos)=>{
                console.log(datos)
                dato_dir = datos.coordenadas
                console.log(dato_dir)
            })
            console.log("si")
        }).catch((res) =>{
            console.log(res)
            console.log("no")
        })
        console.log("si paso")
    }
    
    function inversaPuma(){
        fetch('http://localhost:5001/inversa', {
            method:'POST',
            body: JSON.stringify({
                robot:'puma',
                datos:{
                    x:x,
                    y:y,
                    z:z,
                    d1:d1,
                    d4:d4,
                    a2:a2,
                    d6:d6,
                    alpha:alpha,
                    beta:beta,
                    phi:phi
                }
            })
        }).then((res) =>{
            res.json().then((datos)=>{
                console.log(datos)
                dato_inv = datos.res
                console.log(dato_inv)
            })
            console.log("si")
        }).catch((res) =>{
            console.log(res)
            console.log("no")
        })
        console.log("si paso")
    }

</script>

    <div>
        <h2>Cinemática Robot Puma</h2>
        <div class="contenedor">
            <div class="contenedor-item">
                <h3>Directa</h3>
                <div class="datos">
                    <label for="">&theta 1:</label>
                    <input type="number" bind:value={theta1}>
                    <label for="">&theta 2:</label>
                    <input type="number" bind:value={theta2}>
                    <label for="">&theta 3:</label>
                    <input type="number" bind:value={theta3}>
                    <label for="">&theta 4:</label>
                    <input type="number" bind:value={theta4}>
                    <label for="">&theta 5:</label>
                    <input type="number" bind:value={theta5}>
                    <label for="">&theta 6:</label>
                    <input type="number" bind:value={theta6}>
                </div>
                <button class="calcular" on:click={directaPuma}>Calcular</button>
                <div>
                    <div>
                        <label class="titulo" for="">Posición</label>
                        <label for="">x : {dato_dir.posicion.x}</label>
                        <label for="">y : {dato_dir.posicion.y}</label>
                        <label for="">z : {dato_dir.posicion.z}</label>
                    </div>
                    <div>
                        <label class="titulo" for="">Orientación ZYZ</label>
                        <label for="">z : {dato_dir.orientacion_zyz.alpha}</label>
                        <label for="">y : {dato_dir.orientacion_zyz.beta}</label>
                        <label for="">z : {dato_dir.orientacion_zyz.phi}</label>
                    </div>
                    <div>
                        <label class="titulo" for="">Orientación roll-pitch-yaw</label>
                        <label for="">roll : {dato_dir.orientacion_rpy.roll}</label>
                        <label for="">pitch : {dato_dir.orientacion_rpy.pitch}</label>
                        <label for="">yaw : {dato_dir.orientacion_rpy.yaw}</label>
                    </div>
                </div>
            </div>
            <div class="contenedor-item">
                <h3>Robot</h3>
                <div class="recursos-robot">
                    <button on:click={()=>cambiarRecurso('estructura')} >Estructura</button>
                    <button on:click={()=>cambiarRecurso('animacion')}>Animación</button>
                    <button on:click={()=>cambiarRecurso('real')}>Real</button>
                </div>
                <div class="recurso">
                    {#if resource === 'estructura'}
                    <img src="assets/estructura/puma.png" alt="" >
                    {:else if resource === 'animacion'}
                    <img src="assets/gif/puma.gif" alt="" >
                    {:else}
                    <iframe src="https://www.youtube.com/embed/GcaaZkjVYLo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
                    {/if}

                </div>
                <div class="datos">
                    <label for="">d1:</label>
                    <input type="number" bind:value={d1}>
                    <label for="">a2:</label>
                    <input type="number" bind:value={a2}>
                    <label for="">d4:</label>
                    <input type="number" bind:value={d4}>
                    <label for="">d6:</label>
                    <input type="number" bind:value={d6}>

                </div>
            </div>
            <div class="contenedor-item">
                <h3>Inversa</h3>
                <div class="datos">
                    <label for="">x:</label>
                    <input type="number" bind:value={x}>
                    <label for="">y:</label>
                    <input type="number" bind:value={y}>
                    <label for="">z:</label>
                    <input type="number" bind:value={z}>
                    <label for="">roll:</label>
                    <input type="number" bind:value={alpha}>
                    <label for="">pitch:</label>
                    <input type="number" bind:value={beta}>
                    <label for="">yaw:</label>
                    <input type="number" bind:value={phi}>
                </div>
                <button class="calcular" on:click={inversaPuma}>Calcular</button>
                <div>
                    <div>
                        <label class="titulo" for=""> Ángulos </label>
                        <label for="">&theta 1: {dato_inv.angulos.theta1} </label>
                        <label for="">&theta 2: {dato_inv.angulos.theta2}</label>
                        <label for="">&theta 3: {dato_inv.angulos.theta3}</label>
                        <label for="">&theta 4: {dato_inv.angulos.theta4}</label>
                        <label for="">&theta 5: {dato_inv.angulos.theta5}</label>
                        <label for="">&theta 6: {dato_inv.angulos.theta6}</label>
                    </div>
                    <div>
                        <br>
                        <label class="titulo" for=""> Orientación ZYZ</label>
                        <label for="">z: {dato_inv.orientacion_zyz.alpha_z}</label>
                        <label for="">y: {dato_inv.orientacion_zyz.beta_y}</label>
                        <label for="">z: {dato_inv.orientacion_zyz.phi_z}</label>
                    </div>
                </div>
            </div>
        </div>
    </div>
    

<style>
    .contenedor{
        background-color:rgb(228, 240, 240);
        display: grid;
        grid-template-columns: 25% 45% 25%;
    }
    .contenedor-item{
        margin: 5px;
        border-radius: 2%;
        border: 2px solid rgb(51, 48, 48);
        padding: 5px;
    }

    img, iframe{
        width: 100%;
        height: auto;
        object-fit: cover;

    }
    .recursos-robot{
        display: grid;
        grid-template-columns: repeat(3,1fr);
    }
    .datos{
        display: grid;
        grid-template-columns: 30% 70%;
    }
    h3, h2{
        text-align: center;
    }
    .calcular{
        width: 100%;
    }
    button{
        background-color: rgb(253, 230, 230);
    }
    button:hover{
        background-color: chartreuse;
    }
    .datos label{
        text-align: center;
        margin-top: 5px;
    }
    .titulo{
        margin: 3px;
        background-color: honeydew;
    }
    input{
        border: 1px dotted floralwhite;
        border-radius: 10px;
    }
    

</style>
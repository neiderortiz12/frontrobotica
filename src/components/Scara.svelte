<script>
    let resource = 'estructura'
    
    let x = 0
    let y = 10
    let z = 5
    let alpha = "alpha"
    let beta = "beta"
    let phi = "phi"
    let d1 = 10
    let a1 = 5
    let a2 = 5
    let d3 = 5
    let theta1 =90
    let theta2 =0
    let dato_dir = {
        "coordenadas":{
            "x":0,
            "y":0,
            "z":0
        }
        }
    let dato_inv = {
        "angulos":{
            "theta1":0,
            "theta2":0,
            "d3":0
        }
    }
    function cambiarRecurso(recurso){
        resource=recurso
    }

    function directaScara(){
        fetch('http://localhost:5001/directa', {
            method:'POST',
            body: JSON.stringify({
                robot:'scara',
                datos:{
                    d1:d1,
                    d3:d3,
                    a1:a1,
                    a2:a2,
                    theta1:theta1,
                    theta2:theta2,
                }
            })
        }).then((res) =>{
            res.json().then((datos)=>{
                console.log(datos)
                dato_dir = datos
                console.log(dato_dir)
            })
            console.log("si")
        }).catch((res) =>{
            console.log(res)
            console.log("no")
        })
        console.log("si paso")
    }
    function inversaScara(){
        fetch('http://localhost:5001/inversa', {
            method:'POST',
            body: JSON.stringify({
                robot:'scara',
                datos:{
                    x:x,
                    y:y,
                    z:z,
                    d1:d1,
                    a1:a1,
                    a2:a2,
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
        <h2>Cinemática Robot Scara</h2>
        <div class="contenedor">
            <div class="contenedor-item">
                <h3>Directa</h3>
                <div class="datos">
                    <label for="">d3:</label>
                    <input type="number" bind:value={d3}>
                    <label for="">&theta 1:</label>
                    <input type="number" bind:value={theta1}>
                    <label for="">&theta 2:</label>
                    <input type="number" bind:value={theta2}>
                </div>
                <button class="calcular" on:click={directaScara}>Calcular</button>
                <div>
                    <label class="titulo" for=""> Posición</label>
                    <label for="">x : {dato_dir.coordenadas.x}</label>
                    <label for="">y : {dato_dir.coordenadas.y}</label>
                    <label for="">z : {dato_dir.coordenadas.z}</label>
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
                    <img src="assets/estructura/scara.png" alt="" >
                    {:else if resource === 'animacion'}
                    <img src="assets/gif/scara.gif" alt="" >
                    {:else}
                    <iframe src="https://www.youtube.com/embed/vKD20BTkXhk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
                    {/if}

                </div>
                <div class="datos">
                    <label for="">d1:</label>
                    <input type="number" bind:value={d1}>
                    <label for="">a1:</label>
                    <input type="number" bind:value={a1}>
                    <label for="">a2:</label>
                    <input type="number" bind:value={a2}>
                </div>
            </div>
            <div class="contenedor-item">
                <h3>Inversa</h3>
                <div>
                    <div class="datos">
                        <label for="">x:</label>
                        <input type="number" bind:value={x}>
                        <label for="">y:</label>
                        <input type="number" bind:value={y}>
                        <label for="">z:</label>
                        <input type="number" bind:value={z}>
                    </div>
                    <button class="calcular" on:click={inversaScara}>Calcular</button>
                    <div>
                        <label class="titulo" for=""> Ángulos</label>
                        <label for="">d3: {dato_inv.angulos.d3}</label>
                        <label for="">&theta 1: {dato_inv.angulos.theta1}</label>
                        <label for="">&theta 2: {dato_inv.angulos.theta2}</label>
                    </div>
                </div>
            </div>
        </div>
        
    </div>
    

<style>
    .contenedor{
        background-color:rgb(243, 243, 231);
        display: grid;
        grid-template-columns: 25% 45% 25%;
    }
    
    img, iframe{
        width: 100%;
        height: auto;
        object-fit: cover;

    }
    .contenedor-item{
        margin: 5px;
        border-radius: 2%;
        border: 2px solid rgb(51, 48, 48);
        padding: 5px;
    }
    .recursos-robot{
        display: grid;
        grid-template-columns: repeat(3,1fr);
    }
    .datos{
        display: grid;
        grid-template-columns: 30% 70%;
    }
    button{
        background-color: rgb(253, 230, 230);
    }
    button:hover{
        background-color: chartreuse;
    }
    .calcular{
        width: 100%;
    }
    h3, h2{
        text-align: center;
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
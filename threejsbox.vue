<template>
  <div class="hello" >
  <div style="margin:0 auto;">
AA
  </div>
    <div ref="demo1" v-bind:style="{position:canvas_position,width:'100%', height:'100%',top:canvas_top+'px',margin:'0px',}">
    <div style="z-index:9999;position:absolute;margin:0 auto;width:100%;color:#FFF;" >TitleBar</div>
    </div>
      <div style="height:999rem;color:#FFF;">
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>sampleText<br>SampleText<br>
      </div>

  </div>


</template>

<script>
import * as THREE from 'three'
import FBXLoader from 'three-fbx-loader'
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
   data: () => ({
    controls: {
      scene: null,
      camera: null,
      renderer: null,
      rotationSpeed: 0.01,
      cubephase :0,
    },
    canvas_top:0,
    canvas_position:"fixed",
  }),
  mounted() {
    this.init();
    
    var __this = this;
    window.onresize = function(){ // 定义窗口大小变更通知事件
        __this.resize();
    };

  },
  methods: {
    init () {
      let {initMesh, controls} = this
      
      initMesh()
    },
    resize(){
      
      for(let i=0;i<this.$refs.demo1.children.length;i++)
      {
        console.log(this.$refs.demo1.children[i].nodeName);
        if(this.$refs.demo1.children[i].nodeName=="CANVAS")
        {
          this.$refs.demo1.removeChild(this.$refs.demo1.children[i]);
          continue;
        }
      }

      this.renderer.domElement=null;
      this.renderer=null;
      this.renderer = new THREE.WebGLRenderer({ antialias: true ,alpha:true})// 渲染器
      this.renderer.setClearColor(0x110000,0);
      this.renderer.setSize(window.innerWidth, window.innerHeight - 100)
      this.$refs.demo1.append(this.renderer.domElement)
      this.renderScene()
    },
     initMesh :async function(){
      this.scene = new THREE.Scene() // 场景
      //this.camera = new THREE.OrthographicCamera(-50,50,-50,50,0.1,1000);
      this.camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 1000) // 相机.视场，长宽比，近面，远面
      this.camera.position.x = -20
      this.camera.position.y = 40
      this.camera.position.z = 30
      this.camera.lookAt(this.scene.position)

      this.renderer = new THREE.WebGLRenderer({ antialias: true ,alpha:true})// 渲染器
      this.renderer.setClearColor(0x110000,0);
      this.renderer.setSize(window.innerWidth, window.innerHeight - 100)
      //this.renderer.shadowMapEnabled = true // 开启阴影

      let axes = new THREE.AxisHelper(20) // 坐标轴

      let planeGeometry = new THREE.PlaneGeometry(800, 800, 10, 10) // 生成平面
      let planeMaterial = new THREE.MeshLambertMaterial({color: 0x000}) // 材质
      let plane = new THREE.Mesh(planeGeometry, planeMaterial)
      plane.rotation.x = -0.5 * Math.PI
      plane.position.x = 0
      plane.position.y = -30
      plane.position.z = 0
      plane.receiveShadow = true

      let cubeGeometry = new THREE.CubeGeometry(10, 10, 10)
      //let cubeMaterial = new THREE.MeshLambertMaterial({color: 0xff0000})
     
      let __this=this;
      let texture = await new Promise(function(resolve,reject){
              var loader = new THREE.TextureLoader();
              loader.load('./logo.png',function(texture){
                  resolve(texture);
              });



      }) ;//THREE.ImageUtils.LoadTexture('./logo.png');

      this.fbx_g0 = await new Promise(function(resolve,reject){
        var loader = new FBXLoader();
        loader.load('./s.fbx',function(texture){
            resolve(texture);
        });



      }) ;
      console.log(this.fbx_g0);
      this.fbx_m0 =this.fbx_g0;
      this.fbx_m0.position.x = 0
      this.fbx_m0.position.y = 0
      this.fbx_m0.position.z = 0

      let cubeMaterial = new THREE.MeshLambertMaterial({map: texture});
      
      this.cube = new THREE.Mesh(cubeGeometry,cubeMaterial)
      //__this.plane = new THREE.Mesh(planeGeometry, cubeMaterial)
      this.cube.position.x = 0
      this.cube.position.y = 0
      this.cube.position.z = 0
      this.cube.castShadow = false

     //__this.plane.rotation.x = -0.5 * Math.PI
     //__this.plane.position.x = 0
     //__this.plane.position.y = -30
     //__this.plane.position.z = 0
     //this.scene.add(this.cube)
     this.scene.add(this.fbx_m0)
     //__this.scene.add(__this.plane)

     //console.log(__this.cube);

      
      let spotLight = new THREE.SpotLight(0xffffff)
      spotLight.position.set(-40, 60, -10)
      spotLight.castShadow = true
      let ambientLight= new THREE.AmbientLight(0xffffff)

      //this.scene.add(axes) // 场景添加坐标轴
      //this.scene.add(plane) // 向该场景中添加物体      
      this.scene.add(spotLight)
      this.scene.add(ambientLight)
      this.$refs.demo1.append(this.renderer.domElement)
      this.renderScene()
      //console.log(this);
      
    },
    renderScene () {
      let {controls, cube, scene, camera, renderer} = this
      if(cube==null){
        requestAnimationFrame(this.renderScene)
        return;
        }

      let t=document.documentElement.scrollTop;
      let t_t=document.body.scrollTop;
      if(t_t>t )
      {
        t=t_t;
      }
      let t_f=parseFloat(t);
/////////////////////////////////////////////////////////////
      this.canvas_top=t_f;
      if(this.canvas_top>1500)
      {
        this.canvas_top=1500;
        this.canvas_position="absolute";
      }else{
        this.canvas_position="fixed";
        this.canvas_top=0;
      }
      //console.log(this.canvas_top);
/////////////////////////////////////////////////////////////////
      t_f=Math.pow(t_f,0.525);
      t_f*=40;
      if(t_f>1800)
      {
        t_f=1800;
      }

      
      controls.cubephase+=0.1;
      if(controls.cubephase>3.14)
      {
        controls.cubephase=-3.14;
      }
      //cube.position.y=Math.sin(controls.cubephase)*1.0;
      //console.log( controls.cubephase);
      cube.rotation.x = controls.rotationSpeed*t_f/18*3.14159;
      cube.rotation.y = controls.rotationSpeed*t_f/18*3.14159;
      cube.rotation.z = controls.rotationSpeed*t_f/18*3.14159;
///////////////////////////////////////////////////////////////////////////////
      if (t_f>1720 && t_f<1800)
      {
        cube.position.x=0.4*(parseInt(t_f*1023)%9-4.5);
        cube.position.z=0.4*(parseInt(t_f*511)%9-4.5);
      }else
      {
        cube.position.x=0;
        cube.position.z=0;
      }
/////////////////////////////////////////////////////////////////////////////////

      this.camera.position.x = 0
      this.camera.position.y = 20*(18-t_f/100) +20;
      this.camera.position.z = 0*(18-t_f/100)
      this.camera.lookAt(this.scene.position)
////////////////////////////////////////////////////////////////////////////////
      let opacity= this.clamp(1800-t_f,100,100)/100.0;
      this.cube.material.opacity=opacity;
      //console.log(cube.rotation.z);
      //console.log(cube.rotation.y);
      //console.log(cube.rotation.z);
      requestAnimationFrame(this.renderScene);
      renderer.render(scene, camera)
    },
    clamp(x,l,g)
    {
      if(x<l)
      {
        return l;
      }
      if(x>g)
      {
        return g;
      }
      return x;
    }


  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

##WebGL No.3 - 材质和纹理
###笔记 
#### 纹理加载器  
##### TextureLoader  
当要载入一个外部资源作为纹理贴图的时候需要用到这个方法。 

	//实例化加载器  
	var loader  = new THREE.TextureLoader();
	
	//加载资源
	loader.load(
	     [url],//资源路径
		 function ( texture ) {
			//资源加载成功后的回调函数，texture为加载成功的资源
			//在这里声明材质
			var material = ....

		},
		[onProgress], //资源加载中的回调函数。参数是将处理事件
		[onError], //资源加载错误时的回调函数
	)


注意当资源加载完成后，物体也添加了该材质画布是需要**重新渲染**的,不然会出现添加了材质的物体一片黑的情况。

当要为一个多面体的每一个面都添加不同的材质的时候，需要使用`new THREE.MeshFaceMaterial`

>它接受一个material的数组为参数

当需要一个材质重复时，首先要制定重复的方向

`texture.wrapS = texture.wrapT = THREE.RepeatWrapping;`  
在设置各个方向上的重复次数  
`texture.repeat.set(4,4)`

在添加纹理贴图的时候，控制台还报了如下警告：  
`HREE.WebGLRenderer: image is not power of two (402x273). Resized to 512x256`   
是因为在模型的长宽比和材质的长宽比不符时就会出现这个提示

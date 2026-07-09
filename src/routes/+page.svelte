<script lang="ts">
	import Navbar from '../lib/Navbar.svelte';
	import { onMount } from 'svelte';
    import * as THREE from 'three';
    import {diffuseColor, range} from 'three/tsl';
    import { OrbitControls } from 'three/addons/controls/OrbitControls.js';

    //logo imports
    import svelte_logo from '$lib/images/svelte_logo.png';
    import express_logo from '$lib/images/express_logo.png';
    import lua_logo from '$lib/images/lua_logo.png';
    import node_logo from '$lib/images/node_logo.png';
    import python_logo from '$lib/images/python_logo.png';
    import ts_logo from '$lib/images/ts_logo.png';
    import vue_logo from '$lib/images/vue_logo.png';
    import plex_logo from '$lib/images/plex_logo.png';
    import docker_logo from '$lib/images/docker_logo.png';
    import unifi_logo from '$lib/images/unifi_logo.png';
    import dsm_logo from '$lib/images/dsm_logo.png';
    import ffmpeg_logo from '$lib/images/ffmpeg_logo.png';
    import sonarr_logo from '$lib/images/sonarr_logo.png';
    import radarr_logo from '$lib/images/radarr_logo.png';
    import overseerr_logo from '$lib/images/overseerr_logo.png';
    import prowlarr_logo from '$lib/images/prowlarr_logo.png';
    import bazarr_logo from '$lib/images/bazarr_logo.png';
    import sabnzbd_logo from '$lib/images/sabnzbd_logo.png';
    import proxmox_logo from '$lib/images/proxmox_logo.png';
    import pihole_logo from '$lib/images/pihole_logo.png';
    import threejs_logo from '$lib/images/threejs_logo.png';

    //texture imports
    import water_texture from '$lib/textures/water.jpg';
    import onyx_texture from '$lib/textures/onyx.png';
    import ab_texture from '$lib/textures/ab_one.jpg';
    import stars from '$lib/textures/stars.jpg';
    import astra from '$lib/textures/astra.jpg';
    import kalidescope from '$lib/textures/kalidescope.jpg';
    import pexels_one from '$lib/textures/pexels_one.jpg';
    import white_brick from '$lib/textures/white_brick.jpg';
    import marble from '$lib/textures/marble.jpg';
    import flooring from '$lib/textures/flooring.jpg';
    import sky from '$lib/textures/sky.jpg';

    //pbr textures
    import abstract_nm_import from '$lib/textures/pbr/abstract/abstract_normal.jpg';
    import abstract_ao_import from '$lib/textures/pbr/abstract/abstract_ambient_occlusion.jpg';
    import abstract_cm_import from '$lib/textures/pbr/abstract/abstract_basecolor.jpg';
    import abstract_hm_import from '$lib/textures/pbr/abstract/abstract_height.png';
    import abstract_rm_import from '$lib/textures/pbr/abstract/abstract_roughness.jpg';
    import abstract_m_import from '$lib/textures/pbr/abstract/material.jpg';

    import alien_cm_import from '$lib/textures/pbr/alien/alien_cm.jpg';
    import alien_dm_import from '$lib/textures/pbr/alien/alien_dpm.png';
    import alien_nm_import from '$lib/textures/pbr/alien/alien_nm.jpg';
    import alien_om_import from '$lib/textures/pbr/alien/alien_ocm.jpg';
    import alien_sm_import from '$lib/textures/pbr/alien/alien_spm.jpg';

    import bi_cm_import from '$lib/textures/pbr/water/blue_ice_cm.jpg';
    import bi_dm_import from '$lib/textures/pbr/water/blue_ice_dm.png';
    import bi_nm_import from '$lib/textures/pbr/water/blue_ice_nm.jpg';
    import bi_om_import from '$lib/textures/pbr/water/blue_ice_aom.jpg';
    import bi_rm_import from '$lib/textures/pbr/water/blue_ice_rm.jpg';


	onMount(() => {
		document.body.classList.add('loaded');

        //pbr loaders
        const loader_abstract_normal = new THREE.TextureLoader().load(abstract_nm_import);
        const loader_abstract_ao = new THREE.TextureLoader().load(abstract_ao_import);
        const loader_abstract_bc = new THREE.TextureLoader().load(abstract_cm_import);
        const loader_abstract_height = new THREE.TextureLoader().load(abstract_hm_import);
        const loader_abstract_roughness = new THREE.TextureLoader().load(abstract_rm_import);
        const loader_abstract_material = new THREE.TextureLoader().load(abstract_m_import);

        const alien_nm = new THREE.TextureLoader().load(alien_nm_import);
        const alien_aom = new THREE.TextureLoader().load(alien_om_import);
        const alien_cm = new THREE.TextureLoader().load(alien_cm_import);
        const alien_dm = new THREE.TextureLoader().load(alien_dm_import);
        const alien_sm = new THREE.TextureLoader().load(alien_sm_import);

        const bi_cm = new THREE.TextureLoader().load(bi_cm_import);
        const bi_dm = new THREE.TextureLoader().load(bi_dm_import);
        const bi_nm = new THREE.TextureLoader().load(bi_nm_import);
        const bi_aom = new THREE.TextureLoader().load(bi_om_import);
        const bi_rm = new THREE.TextureLoader().load(bi_rm_import);

        //const texture = new THREE.TextureLoader().load(sky);

        //setup three.js scene, camera and renderer
        const lava_lamp_scene = document.getElementById('lava_lamp_container');
        const ll_scene_width: number = lava_lamp_scene?.offsetWidth ?? 0;
        const ll_scene_height: number = lava_lamp_scene?.offsetHeight ?? 0;
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera( 75, ll_scene_width / ll_scene_height, 0.1, 1000 );
        const timer = new THREE.Timer();

        const renderer = new THREE.WebGLRenderer();
        renderer.setSize( ll_scene_width, ll_scene_height );
        lava_lamp_scene?.appendChild( renderer.domElement );

        //create stars for background
        const stars_count = 2000;
        const star_positions = [];

        for ( let i = 0; i < stars_count; i ++ ) {
            const x = THREE.MathUtils.randFloatSpread( 2000 );
            const y = THREE.MathUtils.randFloatSpread( 2000 );
            const z = THREE.MathUtils.randFloatSpread( 2000 );
            star_positions.push( x, y, z );
        }

        const star = new THREE.BufferGeometry();
        star.setAttribute('position', new THREE.Float32BufferAttribute(star_positions, 3));

        const star_point_mat = new THREE.PointsMaterial({
            color: 0xffffff,
            size: 1,
            sizeAttenuation: true,
        });

        const star_shader_mat = new THREE.ShaderMaterial( {
            uniforms: {
                diffuseColor: { value: new THREE.Color(0xffffff)},
                resolution: { value: new THREE.Vector2() }
            },
            transparent: true,
            depthWrite: false,

        } );


        const stars = new THREE.Points(star, star_point_mat);
        
        //create center planet
        const planet_geo = new THREE.SphereGeometry(40, 128, 64);

        //material defs
        const basic_material = new THREE.MeshBasicMaterial( { color: 0x3a025f, wireframe: true, wireframeLinewidth: 10 } );
        const abstract_mat = new THREE.MeshStandardMaterial({
            map: loader_abstract_bc,
            normalMap: loader_abstract_normal,
            aoMap: loader_abstract_ao,
            roughnessMap: loader_abstract_roughness,
            displacementMap: loader_abstract_height,
            aoMapIntensity: 1,
            roughness: 1,
            metalness: 1,
            alphaTest: 0.0,
            transparent: true,
            wireframe: false
        })

        const alien_mat = new THREE.MeshStandardMaterial({
            map: alien_cm,
            normalMap: alien_nm,
            aoMap: alien_aom,
            roughnessMap: loader_abstract_roughness,
            displacementMap: alien_dm,
            metalnessMap: alien_sm,
            //emissiveMap: alien_sm,
            aoMapIntensity: 1,
            roughness: .7,
            metalness: .2,
            alphaTest: 0.0,
            transparent: true,
            wireframe: false,
            color: 0x8a2be2,
        })

        const bi_mat = new THREE.MeshStandardMaterial({
            map: bi_cm,
            normalMap: bi_nm,
            aoMap: bi_aom,
            roughnessMap: bi_rm,
            displacementMap: bi_dm,
            //emissiveMap: alien_sm,
            aoMapIntensity: 1,
            roughness: 1,
            alphaTest: 0.0,
            transparent: true,
            wireframe: false,
            //color: 0x8a2be2,
        })

/*         const custom_mat = new THREE.MeshStandardMaterial({
            //emissive: 0x000000,
            color: 0x8a2be2,
            roughness: .2,
            metalness: 0.5,
            flatShading: false,
            fog: false,
            //vertexColors: true,
            map: texture,
        }) */

        //applying geometry and material to a mesh
        const planet = new THREE.Mesh(planet_geo, bi_mat);

        //create lighting
        const light = new THREE.AmbientLight( 0xffffff, 1.5 );
        const directional_light = new THREE.DirectionalLight(0xEDB230, 4);
        directional_light.position.set(10, 20, 20);
        const fill_light = new THREE.DirectionalLight(0xEDB230, 2);
        fill_light.position.set(-10, -20, -30);

        //scene additions
        scene.add(light);
        scene.add(directional_light);
        scene.add(fill_light);
        scene.add(planet);
        scene.add(stars);

        //camera positioning
        camera.position.z = 120;
        const controls = new OrbitControls( camera, renderer.domElement );
        camera.position.set( 0, 20, 100 );
        controls.update();

        //default threejs function for drawing and updating objects on the screen
        function animate( time: number ) {
            //sphere.rotation.x = time / 15000;
            planet.rotation.y = time / 15000;
            controls.update();
            renderer.render( scene, camera );
            stars.rotation.y += 0.0002;
        }
        renderer.setAnimationLoop( animate );

    });

    const dev_stack = [
    {
       name: "svelte",
       icon: svelte_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "vue",
       icon: vue_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "express",
       icon: express_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "typescript",
       icon: ts_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "node",
       icon: node_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "threejs",
       icon: threejs_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "python",
       icon: python_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "lua",
       icon: lua_logo,
       height: "100px",
       width: "100px"
    }
]

const homelab_tech = [
    {
       name: "ffmpeg utils",
       icon: ffmpeg_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "docker",
       icon: docker_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "unifi",
       icon: unifi_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "synology",
       icon: dsm_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "sonarr",
       icon: sonarr_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "radarr",
       icon: radarr_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "prowlarr",
       icon: prowlarr_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "overseerr",
       icon: overseerr_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "bazarr",
       icon: bazarr_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "sabnzbd",
       icon: sabnzbd_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "plex",
       icon: plex_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "proxmox",
       icon: proxmox_logo,
       height: "100px",
       width: "100px"
    },
    {
       name: "pihole",
       icon: pihole_logo,
       height: "100px",
       width: "100px"
    }
]


</script>

<div class="content_container">
	<div id="lava_lamp_container">
        
	</div>
	<div class="content_container_child space_grotesk_norm" id="intro_section">
		<p class="content_text">
			Hey, I'm Adam. Sometimes referred to as hamburger.
            <br/><br/>
            Here you can find a list of technologies I am working with and things I am using to push my learning foward.
            I try to keep this site as up to date as possible but sometimes I am too busy with other things as most of you could understand.
            <br/><br/>
            Currently, I am very interested in how graphics are rendered to a screen whether that is on the web or on a deskop. Right now I am choosing to spend my time mainly on learning WebGL and three.js but have plans to dive deeper into OpenGL and pickup some skills using C++.
		</p>
	</div>
    <div class="content_container_child space_grotesk_norm" id="tech_display_icons">
        <h1>Dev stack</h1>
            {#each dev_stack as tech}
                <div class="technology_badge">
                    <span>{tech.name}</span>
                    <div><img src={tech.icon} height={tech.height} width={tech.width} alt="tech icon"/></div>
                </div>
            {/each}
	</div>
        <div class="content_container_child space_grotesk_norm" id="tech_display_icons">
        <h1>Homelab</h1>
            {#each homelab_tech as tech}
                <div class="technology_badge">
                    <span>{tech.name}</span>
                    <div><img src={tech.icon} height={tech.height} width={tech.width} alt="tech icon"/></div>
                </div>
            {/each}
	</div>
</div>

<style>
	:global {
		@import url('https://fonts.googleapis.com/css2?family=Bokor&family=Carter+One&family=Outfit:wght@100..900&family=Rubik+Glitch&family=Space+Grotesk:wght@300..700&display=swap');

		/* color globals */
		:root {
			--creamy: #ffcf9c;
			--indigo: #3a025f;
			--celadon: #a4d4b4;
			--baltic: #035e7b;
			--tomato: #fe5e41;
			--bg: #180e1c;
			--dark_amethyst: #270141;
            --accent: #210237;
		}

        .content_text {
            padding: 3em 0em;
            font-size: 1.5em;
            text-align: justify;
            max-width: 50vw;
        }

		.rubik_glitch_regular {
			font-family: 'Rubik Glitch', system-ui;
			font-weight: 400;
			font-style: normal;
		}

		.outfit_norm {
			font-family: 'Outfit', sans-serif;
			font-optical-sizing: auto;
			font-weight: 600;
			font-style: normal;
		}

		.space_grotesk_norm {
			font-family: 'Space Grotesk', sans-serif;
			font-optical-sizing: auto;
			font-weight: 600;
			font-style: normal;
		}

		.carter_one_regular {
			font-family: 'Carter One', system-ui;
			font-weight: 400;
			font-style: normal;
		}

		.bokor_regular {
			font-family: 'Bokor', system-ui;
			font-weight: 400;
			font-style: normal;
		}

		.site_headers {
			text-align: left;
			justify-content: left;
			font-size: 4em;
			font-weight: 800;
			color: var(--creamy);
			margin-left: 1em;
		}

		.content_container {
            flex: 1;
		}

        .content_container_child {
            display: flex;
            flex-wrap: wrap;
            padding: 1em 5em;
            min-width: 25vw;
            max-width: 95dvw;
            color: var(--creamy);
            flex: 1 0 auto;
            background: #210237;
        }

        .content_container_child h1 {
            width: 100%;
        }
	}

    #lava_lamp_container {
        width: 100vw;
        height: 100vh;
        background: #120318;
    }

    .technology_badge {
        padding: 20px;
        background: var(--accent);
        border: 5px solid var(--creamy);
        border-radius: 20px;
        text-align: center;
        width: 200px;
    }

    .technology_badge span {
        text-transform: uppercase;
        font-weight: 600;
        background: var(--indigo);
        padding: 5px 20px;
        border-radius: 10px;
        display: inline-block;
        width: 100%;
    }

    .technology_badge img {
        margin: 0 auto;
    }

    #tech_display_icons {
        gap: 20px;
        align-items: center;
        background: var(--accent);
    }

    .technology_badge div {
        padding-top: 1.5em;
    }

    .content_container_child h1 {
        font-size: 2em;
        text-transform: uppercase;
    }

    #intro_section {
        justify-content: left;
    }

    @media (width <= 1300px) {
        .content_container_child {
            padding: 1em 2em;
            max-width: 100dvw;

        }

        .content_text {
            padding: 2em 0em;
            font-size: 1.4em;
            text-align: left;
            max-width: 100vw;
        }

        .technology_badge {
            flex: 0 0 45%;
        }

        .technology_badge span {
            padding: 5px 5px;
        }

    }
</style>

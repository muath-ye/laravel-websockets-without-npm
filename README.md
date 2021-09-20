<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400"></a></p>

<p align="center">
<a href="https://travis-ci.org/laravel/framework"><img src="https://travis-ci.org/laravel/framework.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

## This 2 .js files are used to listen from server broadcasting with laravel-websockets, so that you don't need the use of Vue.js in your laravel app

- Follow all installation and configuration process of **laravel-websockets** and instead of using Vue.js component, just add this line where you want to listen for changes :

```javascript


<script>
        window.Laravel = <?php echo json_encode([
            'csrfToken' => csrf_token(),
        ]); ?>;
        var module = { }; /*   <-----THIS LINE */
</script>


<script type="module">

        import Echo from '{{asset('js/echo.js')}}'

        import {Pusher} from '{{asset('js/pusher.js')}}'

        window.Pusher = Pusher

        window.Echo = new Echo({
            broadcaster: 'pusher',
            key: 'your-key',
            wsHost: window.location.hostname,
            wsPort: 6001,
            forceTLS: false,
            disableStats: true,
        });

        window.Echo.channel('your-channel')
        .listen('your-event-class', (e) => {
                console.log(e)
        })

        console.log("websokets in use")

</script> 

```

## To generate them follow this instructions

1. Install laravel-echo and pusher with npm

2. Go to ```your-project-folder/node_modules/laravel-echo/dist``` and copy ```echo.js``` to ```your-project-folder/public/js```

3. Go to ```your-project-folder/node_modules/pusher-js/dist/worker``` and copy ```pusher.worker.js```, rename it to ```pusher.js``` then copy to ```your-project-folder/public/js```

4. To the new ```pusher.js``` renamed add "export" before the "var Pusher" in the first line of code like so:

   > export var Pusher =

Thats it

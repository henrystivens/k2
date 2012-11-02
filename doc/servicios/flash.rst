El servicio Flash
==================

.. contents:: El servicio KumbiaPHP\Flash\Flash nos permite enviar mensajes desde un controlador a una vista, ya sea en la misma petición ó en la siguiente, lo cual es muy util cuando queremos informar al usuario de un evento ocurrido en algun proceso, tambien es muy usado para enviar un mensaje y redirigir a otra página, y en esta, mostrar dicho mensaje si existe.

Métodos del Servicio
--------------------

set()
____
::

    /**
     * Establece un mensaje flash
     * 
     * @param string $type tipo del mensaje ( success, info , error, advertencia )
     * @param string $message  el mensaje a guardar.
     */
    public function set($type, $message)

has()
____
::

    /**
     * Verifica la existencia de un mensaje en la clase, se debe pasar su tipo
     * @param string $type
     * @return boolean 
     */
    public function has($type)

get()
____
::

    /**
     * Devuelve un mensaje que ha sido previamente guardado, si existe.
     * 
     * antes de devolver el mensaje lo borra de la sesión.
     * 
     * @param string $type
     * @return string|NULL 
     */
    public function get($type)

getAll()
_______
::

    /**
     * Devuelve todos los mensajes guardados previamente y los borra
     * de la session.
     * 
     * @return array arreglo donde los indices son el tipo de mensaje y el valor
     * es el contenido del mensaje. 
     */
    public function getAll()

success()
________
::

    /**
     * Establece un mensaje de tipo success
     * @param string $message 
     */
    public function success($message)

info()
_____
::

    /**
     * Establece un mensaje de tipo info
     * @param type $message 
     */
    public function info($message)

warning()
________
::
    
    /**
     * Establece un mensaje de tipo warning
     * @param string $message 
     */
    public function warning($message)

error()
______
::

    /**
     * Establece un mensaje de tipo error
     * @param string $message 
     */
    public function error($message)

Ejemplo de Uso
--------------

En el siguiente ejemplo enviaremos 1 mensaje de información desde un controlador.
::
    <?php

    namespace MiModulo\Controller;

    use KumbiaPHP\Kernel\Controller\Controller;

    class UsuariosController extends Controller
    {
        public function index()
        {
            $this->get("flash")->info("Lista de Usuarios Vacía...!!!");
        }
    }

    // en la vista leemos el flash

    <?php if (View::flash()->has("info"))://se puede obviar el if, ya que si no existe se muestra vacio ?>
        <?php echo View::flash()->get("info"); ?>
    <?php endif; ?>

    //tambien se pueden imprimir todos los mensajes:

    <?php foreach(View::flash()->getAll() as $type => $msj): ?>
        <div class="<?php echo $type ?>"><?php echo $msj ?></div>
    <?php endforeach; ?>

    //Ó mas facil aun, podemos dejar que la libreria View imprima todos los mensajes por nosotros,
    //solo debemos pasar un true al llamar al método View::content(true) de siempre.

    <?php View::content(true); //pasando true como parametro se imprimiran todos los mensajes flash enviados. ?>

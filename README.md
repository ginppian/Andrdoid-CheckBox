Android CheckBox
============

## Descripción

<p align="center">
	<img src="https://github.com/ginppian/Andrdoid-CheckBox/blob/master/imgs/img1.png" width="270" height="480">
</p>

<p align="justify">
	Buscamos guardar el correo y la contraseña del usuario a través de un CheckBox.
</p>

## Desarrollo

<p align="justify">
	1. Empezamos por la inteface gráfica agregando el <i>CheckBox</i>
</p>

```java
        <CheckBox android:id="@+id/checkbox1"
            android:layout_width="match_parent"
            android:layout_height="55sp"
            android:layout_marginLeft="13sp"
            android:layout_marginRight="13sp"
            android:text="Recordar"
            android:onClick="onCheckboxClicked"/>
```

<p align="justify">
	A nuestro Layout
</p>

```java
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context="mx.paracrecer.paracrecer1.MainActivity">

    <ImageView
        android:id="@+id/imageView"
        android:layout_width="match_parent"
        android:layout_height="110dp"
        android:layout_gravity="center"
        android:layout_marginBottom="34sp"
        android:scaleType="fitCenter"
        android:paddingTop="33dp"
        android:src="@drawable/logo"
        />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="102dp"
        android:orientation="horizontal">

        <ImageView
            android:id="@+id/imageView2"
            android:layout_width="55sp"
            android:layout_height="47sp"
            android:paddingLeft="11sp"
            android:src="@drawable/user"
            />

        <EditText
            android:id="@+id/editText"
            android:layout_width="290dp"
            android:layout_height="wrap_content"
            android:ems="10"
            android:inputType="textPersonName"
            android:paddingLeft="8sp"
            android:paddingRight="28sp"
            android:hint="nombre@paracrecer.mx"
            tools:layout_editor_absoluteX="118dp"
            tools:layout_editor_absoluteY="242dp"
            />

    </LinearLayout>


    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="102dp"
        android:orientation="horizontal">
        <ImageView
            android:id="@+id/imageView3"
            android:layout_width="60sp"
            android:layout_height="50sp"
            android:paddingLeft="7sp"
            android:src="@drawable/pass"
            />

        <EditText
            android:id="@+id/editText2"
            android:layout_width="290dp"
            android:layout_height="wrap_content"
            android:ems="10"
            android:inputType="textPassword"
            android:paddingLeft="8sp"
            android:paddingRight="10sp"
            android:hint="*****"
            tools:layout_editor_absoluteX="118dp"
            tools:layout_editor_absoluteY="312dp"
            />
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="55dp"
        android:orientation="horizontal"
        android:layout_marginTop="-21dp"
        >

        <CheckBox android:id="@+id/checkbox1"
            android:layout_width="match_parent"
            android:layout_height="55sp"
            android:layout_marginLeft="13sp"
            android:layout_marginRight="13sp"
            android:text="Recordar"
            android:onClick="onCheckboxClicked"/>
    </LinearLayout>

    <Button
        android:id="@+id/button"
        android:layout_width="match_parent"
        android:layout_height="33dp"
        android:text="Login"
        android:layout_margin="13sp"
        tools:layout_editor_absoluteY="430dp"
        tools:layout_editor_absoluteX="16dp"
        android:layout_weight="0.17"
        android:clickable="true"
        />

</LinearLayout>

```

<p align="justify">
2. Declaramos una variable del tipo <i>CheckBox</i> y la cargamos al iniciar.
</p>


```java
public class MainActivity extends AppCompatActivity {

    // UI
    private ImageView imgLogo;
    private ImageView imgPerfil;
    private ImageView imgPass;
    private EditText inputPerfil;
    private EditText inputPass;
    private Button boton;
    private CheckBox check;
    private ProgressDialog progress;

        @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // UI
        loadView();
    }
```

```java
    private void loadView(){

        imgLogo = (ImageView) findViewById(R.id.imageView);
        imgPerfil = (ImageView) findViewById(R.id.imageView2);
        imgPass = (ImageView) findViewById(R.id.imageView3);
        inputPerfil = (EditText) findViewById(R.id.editText);
        inputPass = (EditText) findViewById(R.id.editText2);
        boton = (Button) findViewById(R.id.button);
        check = (CheckBox) findViewById(R.id.checkbox1);

        load_RememberData();
    }
```

<p align="justify">
3. Supongamos que ya ha guardado sus datos queremos que cuando empieze la aplicación cargue sus datos entonces agregamos <i>load_RememberData()</i>. Sino simplemente las cajas de texto las dejamos vacias y el check desactivado.
</p>

```java
    private void load_RememberData(){
        SharedPreferences prefs = PreferenceManager.getDefaultSharedPreferences(getApplicationContext());
        String _check = prefs.getString("key_check", "defaultStringIfNothingFound");
        String _correo = prefs.getString("key_correo", "defaultStringIfNothingFound");
        String _password = prefs.getString("key_password", "defaultStringIfNothingFound");

        if(_check.equals("active")){

            inputPerfil.setText(_correo);
            inputPass.setText(_password);
            check.setChecked(true);
        } else {
            inputPerfil.setText("");
            inputPass.setText("");
            check.setChecked(false);
        }
    }
```

<p align="justify">
4. Supongamos que ahora presta el celular a un compañero para que inicie sesión y el compañero por error selecciona <i>Recordar</i> o <i>Activa el Check</i> y se arrepiente y desactiva el check. 
</p>

<p align="justify">
	Tenemos una función que continuamente está sondeando el <i>Check</i> que es <i>onCheckboxClicked</i> como lo especificamos en el <i>Layout</i>
</p>

* ¿Qué pasa si nuestro compañero le dio guardar por error? si metieramos el código de guardar en esta función que sondea ya se hubieran guardado sus datos.

* ¿Qué pasa si por error se guardaron los datos de nuestro compañero? desactivariamos el *Check*, pondriamos nuestros datos y entrariamos.

<p align="justify">Implementamos nuestra función de la siguiente manera</p>

```java
public void onCheckboxClicked(View view){

        // Is the view now checked?
        boolean checked = ((CheckBox) view).isChecked();

        if (checked){
        	// Do nothing ...
        }else{

            SharedPreferences.Editor prefEditor = PreferenceManager.getDefaultSharedPreferences(getApplicationContext()).edit();
            prefEditor.putString("key_correo", "");
            prefEditor.putString("key_password", "");
            prefEditor.putString("key_check", "");
            prefEditor.apply();

        }
    }
```

<p align="justify">
5. ¿Y en qué momento guardamos los datos? Ha pues al hacer click en el boton de <i>Login</i>. Obviamente nuestro login va y consume un servicio y en lo que se consume este servico aparece una Ventana de Progreso mientras el Servicio lo consume en Background. Es por eso que para hacer el proceso en Background creamos un hilo. Bueno si el login es exitoso antes de pasar a la siguiente ventana <b>Guardamos sus datos</b> claro obviamente si el <i>Check</i> está acivado, es decir si el usuario.
</p>

```java
 private void userValidation(){

        // Start progress UI
        progress = new ProgressDialog(MainActivity.this);
        progress.setIndeterminate(true);
        progress.setMessage("Autenticando...");
        progress.show();

        final Thread t = new Thread() {
            @Override
            public void run() {

                // Get value
                String correo = inputPerfil.getText().toString();
                String password = inputPass.getText().toString();

                // Login
                loginSinAsync(correo, password);

                // Stop progress
                progress.dismiss();

                // Change Activity
                if(authorize){

                	// Save user data
                    if(check.isChecked()){

                        SharedPreferences.Editor prefEditor = PreferenceManager.getDefaultSharedPreferences(getApplicationContext()).edit();
                        prefEditor.putString("key_correo", correo);
                        prefEditor.putString("key_password", password);
                        prefEditor.putString("key_check", "active");
                        prefEditor.apply();
                    }

                    try{

                        //Intent intent = new Intent(MainActivity.this, Ubicacion.class);
                        Intent intent = new Intent(MainActivity.this, MapsActivity.class);
                        intent.putExtra("miCorreo", correo);
                        intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
                        intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
                        startActivity(intent);
                        finish();

                    }catch(Exception e){
                        Log.d("what",e.getMessage());
                    }
                } else {

                    // Si no se pudo hacer login
                    // Corremos el Toast en el hilo principal

                    runOnUiThread(new Runnable() {
                        public void run()
                        {
                            Toast.makeText(
                                    getBaseContext(),
                                    "Usuario O Contraseña Incorrectos",
                                    Toast.LENGTH_LONG).
                                    show();
                        }
                    });
                }
            }
        };
        t.start();
    }
```
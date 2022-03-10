##Comando para certificado SSH
keytool -list -v -keystore C:\Users\gabri\.android\debug.keystore -alias androiddebugkey -storepass android -keypass android

[Conexão Facebook](https://www.youtube.com/watch?v=yPe50kXmlPA&t=186s)

[Assinar App Para Publicar na Playstore](https://www.youtube.com/watch?v=MjpaSGEmQHs&t=113s)

## Assinar App
#### Criar a Assinatura
no Android Studio Barra de tarefas:
Tools -> Flutter -> Open Editing in Android Studio 
{New Windows}
Build -> Generate Signed Bulndle/Apk

#### ANDROID\
Criar Arquivo `key.properties`
com conteudo:
storePassword={senha do passo anterior}
keyPassword={senha do passo anterior}  
keyAlias={do passo anterior}
storeFile={caminho do .jks}

#### APP\BUILD.GRADLE
`apply from: "$flutterRoot/packages/flutter_tools/gradle/flutter.gradle"`
  
def keystoreProperties = new Properties()  
def keystorePropertiesFile = rootProject.file('key.properties')  
if (keystorePropertiesFile.exists()) {  
    keystoreProperties.load(new FileInputStream(keystorePropertiesFile))  
}  
  
`android {`

### Colocar abaixo do `defaultConfig{}`
`signingConfigs {  
 release{  
 keyAlias keystoreProperties['keyAlias']  
        keyPassword keystoreProperties['keyPassword']  
        storeFile keystoreProperties['storeFile'] ? file(keystoreProperties['storeFile']) : null  
 storePassword keystoreProperties['storePassword']  
    }  
}
`

buildTypes {  
 release {  
 // TODO: Add your own signing config for the release build.  
 // Signing with the debug keys for now, so `flutter run --release` works.  
 signingConfig signingConfigs.release  
    }  
}

### Gerar AAB
Repetir o Passo de Criar assinatura, dessa vez escolhendo o a key ja criada
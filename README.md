# Ejercicio-4-Cambio-de-Temaf
Ejercicio 4: Cambio de Tema

//Main Act
package com.mexiti.listacomidaor

import android.annotation.SuppressLint
import android.os.Bundle
import android.view.Menu
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.Image
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Row
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.foundation.layout.height
import androidx.compose.foundation.layout.padding
import androidx.compose.foundation.layout.size
import androidx.compose.foundation.lazy.LazyColumn
import androidx.compose.foundation.lazy.items
import androidx.compose.material3.Card
import androidx.compose.material3.CenterAlignedTopAppBar
import androidx.compose.material3.ExperimentalMaterial3Api
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.Scaffold
import androidx.compose.material3.Surface
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.draw.clip
import androidx.compose.ui.layout.ContentScale
import androidx.compose.ui.modifier.modifierLocalConsumer
import androidx.compose.ui.platform.LocalContext
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.res.stringResource
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import com.mexiti.listacomidaor.data.DataSource
import com.mexiti.listacomidaor.model.Platillo
import com.mexiti.listacomidaor.ui.theme.ListaComidaOrTheme

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            ListaComidaOrTheme {
                // A surface container using the 'background' color from the theme
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    MenuApp()
                }
            }
        }
    }
}

@Composable
fun MenuApp(){
    MenuCardList(platilloList = DataSource().LoadPlatillos())
}

@SuppressLint("UnusedMaterial3ScaffoldPaddingParameter")
@Composable
fun MenuCardList( platilloList: List<Platillo>,modifier: Modifier= Modifier   ) {

    Scaffold(
        topBar = {
            MenuTopAppBar()
        }
    ) {
it->
        LazyColumn(contentPadding = it) {      //va a haber un padding entre los lazy column yel scaffold va a estar arriba (organiza)
            items(platilloList) { platillo ->
                MenuCard(
                    platillo = platillo,
                    modifier = modifier.padding(10.dp)
                )
            }

        }

    }
}
@Composable
fun MenuCard(platillo:Platillo, modifier: Modifier = Modifier ){
    Card {
        Column {
            Image(
                painter = painterResource(id = platillo.drawableResourceId) ,
                contentDescription = stringResource(id = platillo.stringResourceId),
                modifier =
                modifier
                    .fillMaxWidth()
                    .height(190.dp),
                contentScale = ContentScale.Crop

            )
            Text(
                text = LocalContext.current.getString(platillo.stringResourceId),
                modifier = modifier.padding(22.dp),
                style = MaterialTheme.typography.displayMedium
            )
            
        }

    }
}
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun MenuTopAppBar(modifier: Modifier= Modifier){
    CenterAlignedTopAppBar(
        title = {
            Row(verticalAlignment =  Alignment.CenterVertically){//centrar texto lista comidaor
                Image(painter = painterResource(id = R.drawable.restaurant) ,
                    contentDescription = null,
                    modifier= modifier
                        .padding(8.dp)
                        .size(64.dp)
                )
                Text(
                    text = stringResource(id = R.string.app_name),
                    style = MaterialTheme.typography.displayLarge
                    )
            }
        },
        modifier= modifier
    )
}


@Composable
@Preview(showBackground = true)
fun ShowMenuCard(){
    ListaComidaOrTheme(darkTheme = true) {

        MenuCardList(platilloList = DataSource().LoadPlatillos()  )
    }

}

//Type
package com.mexiti.listacomidaor.ui.theme

import androidx.compose.material3.Typography
import androidx.compose.ui.text.TextStyle
import androidx.compose.ui.text.font.Font
import androidx.compose.ui.text.font.FontFamily
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.sp
import com.mexiti.listacomidaor.R

// Set of Material typography styles to start with

val AbrilFatFace = FontFamily(
    Font(R.font.kodemonoregular)
)

val Montserrat= FontFamily(
    Font(R.font.kodemonoregular),
    Font(R.font.kodemonobold)
)


//Set of Material typography styles to start with


val Typography = Typography(
    displayLarge = TextStyle(
        fontFamily = AbrilFatFace,
        fontWeight = FontWeight.Normal,
        fontSize = 36.sp
    ),

    displayMedium = TextStyle(
        fontFamily = Montserrat,
        fontWeight = FontWeight.Bold,
        fontSize = 20.sp
    ),

    labelSmall = TextStyle(
        fontFamily = Montserrat,
        fontWeight = FontWeight.Bold,
        fontSize = 20.sp
    ),


    bodyLarge = TextStyle(
        fontFamily = Montserrat,
        fontWeight = FontWeight.Normal,
        fontSize = 20.sp
    ),
 )


 //Color
 package com.mexiti.listacomidaor.ui.theme

import androidx.compose.ui.graphics.Color

val md_theme_light_primary = Color(0xFF00934B)
val md_theme_light_onPrimary = Color(0xFFFFFFFF)
val md_theme_light_primaryContainer = Color(0xFFFFDCC5)
val md_theme_light_onPrimaryContainer = Color(0xFF301400)
val md_theme_light_secondary = Color(0xFF6650A4)
val md_theme_light_onSecondary = Color(0xFFFFFFFF)
val md_theme_light_secondaryContainer = Color(0xFFE8DDFF)
val md_theme_light_onSecondaryContainer = Color(0xFF22005D)
val md_theme_light_tertiary = Color(0xFF5E6135)
val md_theme_light_onTertiary = Color(0xFFFFFFFF)
val md_theme_light_tertiaryContainer = Color(0xFFE4E6AF)
val md_theme_light_onTertiaryContainer = Color(0xFF1B1D00)
val md_theme_light_error = Color(0xFFBA1A1A)
val md_theme_light_errorContainer = Color(0xFFFFDAD6)
val md_theme_light_onError = Color(0xFFFFFFFF)
val md_theme_light_onErrorContainer = Color(0xFF410002)
val md_theme_light_background = Color(0xFFFFFBFF)
val md_theme_light_onBackground = Color(0xFF201A17)
val md_theme_light_surface = Color(0xFFFFFBFF)
val md_theme_light_onSurface = Color(0xFF201A17)
val md_theme_light_surfaceVariant = Color(0xFFF3DFD2)
val md_theme_light_onSurfaceVariant = Color(0xFF52443B)
val md_theme_light_outline = Color(0xFF84746A)
val md_theme_light_inverseOnSurface = Color(0xFFFBEEE8)
val md_theme_light_inverseSurface = Color(0xFF362F2B)
val md_theme_light_inversePrimary = Color(0xFFFFB782)
val md_theme_light_shadow = Color(0xFF000000)
val md_theme_light_surfaceTint = Color(0xFF934B00)
val md_theme_light_outlineVariant = Color(0xFFD6C3B7)
val md_theme_light_scrim = Color(0xFF000000)

val md_theme_dark_primary = Color(0xFFFFB782)
val md_theme_dark_onPrimary = Color(0xFF4F2500)
val md_theme_dark_primaryContainer = Color(0xFF703800)
val md_theme_dark_onPrimaryContainer = Color(0xFFFFDCC5)
val md_theme_dark_secondary = Color(0xFFCFBDFF)
val md_theme_dark_onSecondary = Color(0xFF371E73)
val md_theme_dark_secondaryContainer = Color(0xFF4E378B)
val md_theme_dark_onSecondaryContainer = Color(0xFFE8DDFF)
val md_theme_dark_tertiary = Color(0xFFC7CA95)
val md_theme_dark_onTertiary = Color(0xFF30330B)
val md_theme_dark_tertiaryContainer = Color(0xFF464920)
val md_theme_dark_onTertiaryContainer = Color(0xFFE4E6AF)
val md_theme_dark_error = Color(0xFFFFB4AB)
val md_theme_dark_errorContainer = Color(0xFF93000A)
val md_theme_dark_onError = Color(0xFF690005)
val md_theme_dark_onErrorContainer = Color(0xFFFFDAD6)
val md_theme_dark_background = Color(0xFF201A17)
val md_theme_dark_onBackground = Color(0xFFECE0DA)
val md_theme_dark_surface = Color(0xFF201A17)
val md_theme_dark_onSurface = Color(0xFFECE0DA)
val md_theme_dark_surfaceVariant = Color(0xFF52443B)
val md_theme_dark_onSurfaceVariant = Color(0xFFD6C3B7)
val md_theme_dark_outline = Color(0xFF9F8D83)
val md_theme_dark_inverseOnSurface = Color(0xFF201A17)
val md_theme_dark_inverseSurface = Color(0xFFECE0DA)
val md_theme_dark_inversePrimary = Color(0xFF934B00)
val md_theme_dark_shadow = Color(0xFF000000)
val md_theme_dark_surfaceTint = Color(0xFFFFB782)
val md_theme_dark_outlineVariant = Color(0xFF52443B)
val md_theme_dark_scrim = Color(0xFF000000)


val seed = Color(0xFFEE8933)

//Theme

    outlineVariant = md_theme_light_outlineVariant,
    scrim = md_theme_light_scrim,
)


private val DarkColors = darkColorScheme(
    primary = md_theme_dark_primary,
    onPrimary = md_theme_dark_onPrimary,
    primaryContainer = md_theme_dark_primaryContainer,
    onPrimaryContainer = md_theme_dark_onPrimaryContainer,
    secondary = md_theme_dark_secondary,
    onSecondary = md_theme_dark_onSecondary,
    secondaryContainer = md_theme_dark_secondaryContainer,
    onSecondaryContainer = md_theme_dark_onSecondaryContainer,
    tertiary = md_theme_dark_tertiary,
    onTertiary = md_theme_dark_onTertiary,
    tertiaryContainer = md_theme_dark_tertiaryContainer,
    onTertiaryContainer = md_theme_dark_onTertiaryContainer,
    error = md_theme_dark_error,
    errorContainer = md_theme_dark_errorContainer,
    onError = md_theme_dark_onError,
    onErrorContainer = md_theme_dark_onErrorContainer,
    background = md_theme_dark_background,
    onBackground = md_theme_dark_onBackground,
    surface = md_theme_dark_surface,
    onSurface = md_theme_dark_onSurface,
    surfaceVariant = md_theme_dark_surfaceVariant,
    onSurfaceVariant = md_theme_dark_onSurfaceVariant,
    outline = md_theme_dark_outline,
    inverseOnSurface = md_theme_dark_inverseOnSurface,
    inverseSurface = md_theme_dark_inverseSurface,
    inversePrimary = md_theme_dark_inversePrimary,
    surfaceTint = md_theme_dark_surfaceTint,
    outlineVariant = md_theme_dark_outlineVariant,
    scrim = md_theme_dark_scrim,
)

@Composable
fun ListaComidaOrTheme(
    darkTheme: Boolean = isSystemInDarkTheme(),
    // Dynamic color is available on Android 12+
    dynamicColor: Boolean = false,
    content: @Composable () -> Unit
) {

    val colorScheme = when {
        dynamicColor && Build.VERSION.SDK_INT >= Build.VERSION_CODES.S -> {
            val context = LocalContext.current
            if (darkTheme) dynamicDarkColorScheme(context) else dynamicLightColorScheme(context)
        }

        darkTheme -> DarkColors
        else -> DarkColors
    }
    val view = LocalView.current
    if (!view.isInEditMode) {
        SideEffect {
            val window = (view.context as Activity).window
            window.statusBarColor = colorScheme.primary.toArgb()
            WindowCompat.getInsetsController(window, view).isAppearanceLightStatusBars = darkTheme
        }
    }

    MaterialTheme(
        colorScheme = colorScheme,
        typography = Typography,
        content = content
    )
}

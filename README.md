# ComposeMonet
Material You dynamic color theming with native codes in Jetpack Compose

#Usages

1. Include **lib-release.aar** to your project.

2. Add this line to your Application:
```kotlin
System.loadLibrary("monet")
```

3. MonetTheme.kt
```kotlin
@Composable
fun MonetTheme(content: @Composable () -> Unit) {
    val color = if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.S) {
        colorResource(id = android.R.color.system_accent1_500)
    } else Color(0xFF007FAC)

    CompositionLocalProvider(LocalTonalPalettes provides TonalPalettes(keyColor = color)) {
        CompositionLocalProvider(LocalContentColor provides 0.n1..100.n1) {
            MaterialTheme(content = content)
        }
    }
}
```

4. Use dynamic color in your Composables
```kotlin
0.a1 // accent 1 color with 0% lightness (black)
50.n1 // neutral 1 color with 50% lightness (mid-gray)
100.a3 // accent 3 color with 0% lightness (white)

40.a1..80.a1 // <light-theme-color>..<night-theme-color>
```

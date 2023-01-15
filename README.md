# Compose Monet
Material You dynamic color theming library with native codes in Jetpack Compose.

🚧 Current API is incubating and may change now.

![Screenshot_20221222-135543_Monet](https://user-images.githubusercontent.com/76829190/209067291-5e91eb87-ce53-4964-9eb5-9856bed83a28.png)

## Compatibilities

- **Architectures:** arm64-v8a, x64
- **Android:** 5.0+

## Usages

1. Download and include [**monet.aar**](https://github.com/Kyant0/ComposeMonet/blob/main/monet.aar) to your project.

2. Load native library in your Application
```kotlin
System.loadLibrary("monet")
```

3. Change your compose theme like this example
```kotlin
@Composable
fun MonetTheme(content: @Composable () -> Unit) {
    // key color
    val color = if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.S) {
        colorResource(id = android.R.color.system_accent1_500)
    } else Color(0xFF007FAC)

    CompositionLocalProvider(
        LocalTonalPalettes provides TonalPalettes(
            keyColor = color,
            // There are several styles for TonalPalettes
            // PaletteStyle.TonalSpot for default, .Spritz for muted style, .Vibrant for vibrant style,...
            style = PaletteStyle.TonalSpot
        )
    ) {
        CompositionLocalProvider(LocalContentColor provides 0.n1..100.n1) {
            MaterialTheme(
                colorScheme = dynamicColorScheme(), // Optional if you don't use m3
                content = content
            )
        }
    }
}
```

4. Use dynamic colors in your Composables.
```kotlin
0.a1 // accent 1 color with 0% lightness (black)
50.n1 // neutral 1 color with 50% lightness (mid-gray)
100.a3 // accent 3 color with 0% lightness (white)

40.a1..80.a1 // <light-theme-color>..<dark-theme-color>
```

## Advanced Usages

### Color Harmony
```kotlin
Color.Blue.harmonized(90.0) // harmonize blue color towards 90 hue
```
### Color Extraction from Bitmap
```kotlin
ImageBitmap.getKeyColors(k: Int): List<Color>
```

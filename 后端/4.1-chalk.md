> Create by **fall** on 2022
> Recently revised in 2022-02-08

## chalk

npm 中的一个包，负责控制台高亮



### Colors

`black` `red` `green` `yellow` `blue` `magenta` `cyan` `white` `blackBright` (alias: `gray`, `grey`) `redBright` `greenBright` `yellowBright` `blueBright` `magentaBright` `cyanBright` `whiteBright` 

### Background colors

`bgBlack` `bgRed` `bgGreen` `bgYellow` `bgBlue` `bgMagenta` `bgCyan` `bgWhite` `bgBlackBright` (alias: `bgGray`, `bgGrey`) `bgRedBright` `bgGreenBright` `bgYellowBright` `bgBlueBright` `bgMagentaBright` `bgCyanBright` `bgWhiteBright`

### Modifiers

 `reset` - Reset the current style. `bold` - Make the text bold. `dim` - Make the text have lower opacity. `italic` - Make the text italic. *(Not widely supported)*  `underline` - Put a horizontal line below the text. *(Not widely supported)*  `overline` - Put a horizontal line above the text. *(Not widely supported)*  `inverse`- Invert background and foreground colors. `hidden` - Print the text but make it invisible. `strikethrough` - Puts a horizontal line through the center of the text. *(Not widely supported)*  `visible`- Print the text only when Chalk has a color level above zero. Can be useful for things that are purely cosmetic.
# ![](https://pdf2htmlEX.github.io/pdf2htmlEX/images/pdf2htmlEX-64x64.png) pdf2htmlEX 

[![Build Status](https://travis-ci.org/pdf2htmlEX/pdf2htmlEX.svg?branch=master)](https://travis-ci.org/pdf2htmlEX/pdf2htmlEX)

# Differences from upstream pdf2htmlEX: 

This is my branch of pdf2htmlEX which aims to allow an open collaboration to help keep the project active. A number of changes and improvements have been incorporated from other forks:

* Lots of bugs fixes, mostly of edge cases
* Integration of latest Cairo code
* Out of source building
* Rewritten handling of obscured/partially obscured text - now much more accurate
* Some support for transparent text
* Improvement of DPI settings - clamping of DPI to ensure output graphic isn't too big

`--correct-text-visibility` tracks the visibility of 4 sample points for each character (currently the 4 corners of the character's bounding box, inset slightly) to determine visibility.
It now has two modes. 1 = Fully occluded text handled (i.e. doesn't get put into the HTML layer). 2 = Partially occluded text handled.

The default is now "1", so fully occluded text should no longer show through. If "2" is selected then if the character is partially occluded it will be drawn in the background layer. In this case, the rendered DPI of the page will be automatically increased to `--covered-text-dpi` (default: 300) to reduce the impact of rasterized text.

For maximum accuracy I strongly recommend using the output options: `--font-size-multiplier 1 --zoom 25`. This will circumvent rounding errors inside web browsers. You will then have to scale down the resulting HTML page using an appropriate "scale" transform.

If you are concerned about file size of the resulting HTML, then I recommend patching fontforge to prevent it writing the current time into the dumped fonts, and then post-process the pdf2htmlEX data to remove duplicate files - there will usually be many duplicate background images and fonts.


>一图胜千言<br>A beautiful demo is worth a thousand words

- **Bible de Genève, 1564** (fonts and typography): [HTML](https://pdf2htmlEX.github.io/pdf2htmlEX/demo/geneve.html) / [PDF](https://github.com/raphink/geneve_1564/releases/download/2015-07-08_01/geneve_1564.pdf)
- **Cheat Sheet** (math formulas): [HTML](https://pdf2htmlEX.github.io/pdf2htmlEX/demo/cheat.html) / [PDF](http://www.tug.org/texshowcase/cheat.pdf)
- **Scientific Paper** (text and figures): [HTML](https://pdf2htmlEX.github.io/pdf2htmlEX/demo/demo.html) / [PDF](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.148.349&rep=rep1&type=pdf)
- **Full Circle Magazine** (read while downloading): [HTML](https://pdf2htmlEX.github.io/pdf2htmlEX/demo/issue65_en.html) / [PDF](http://dl.fullcirclemagazine.org/issue65_en.pdf)
- **Git Manual** (CJK support): [HTML](https://pdf2htmlEX.github.io/pdf2htmlEX/demo/chn.html) / [PDF](http://files.cnblogs.com/phphuaibei/git%E6%90%AD%E5%BB%BA.pdf)

pdf2htmlEX renders PDF files in HTML, utilizing modern Web technologies.
Academic papers with lots of formulas and figures? Magazines with complicated layouts? No problem!

pdf2htmlEX is also an [online publishing tool](https://pdf2htmlEX.github.io/pdf2htmlEX/doc/tb108wang.html) which is flexible for many different use cases. 

Learn more about [who](https://github.com/pdf2htmlEX/pdf2htmlEX/wiki/Use-Cases) and [why](https://github.com/pdf2htmlEX/pdf2htmlEX/wiki/Introduction) should use pdf2htmlEX.

### Features

* Native HTML text with precise font and location.
* Flexible output: all-in-one HTML or on demand page loading (needs JavaScript).
* Moderate file size, sometimes even smaller than PDF.
* Supporting links, outlines (bookmarks), printing, SVG background, Type 3 fonts and [more...](https://github.com/pdf2htmlEX/pdf2htmlEX/wiki/Feature-List)

[Compare to others](https://github.com/pdf2htmlEX/pdf2htmlEX/wiki/Comparison)

### Portals

 * [:house:Wiki Home](https://github.com/pdf2htmlEX/pdf2htmlEX/wiki)
 * [Download](https://github.com/pdf2htmlEX/pdf2htmlEX/wiki/Download) & [Building](https://github.com/pdf2htmlEX/pdf2htmlEX/wiki/Building)
 * [Quick Start](https://github.com/pdf2htmlEX/pdf2htmlEX/wiki/Quick-Start)
 * [Report Issues / Ask for Help](https://github.com/pdf2htmlEX/pdf2htmlEX/blob/master/CONTRIBUTING.md#guidance)
 * [:question:FAQ](https://github.com/pdf2htmlEX/pdf2htmlEX/wiki/FAQ)
 * [:envelope:Mailing List](https://groups.google.com/forum/#!forum/pdf2htmlex)
 * [:mahjong:中文邮件列表](https://groups.google.com/forum/#!forum/pdf2htmlex-cn)

### LICENSE

pdf2htmlEX, as a whole package, is licensed under GPLv3+.
Some resource files are released with relaxed licenses, read `LICENSE` for more details.

### Acknowledgements

pdf2htmlEX is made possible thanks to the following projects:

* [poppler](http://poppler.freedesktop.org/)
* [Fontforge](http://fontforge.org/)

[![Testing Powered By SauceLabs](https://saucelabs.github.io/images/opensauce/powered-by-saucelabs-badge-gray.png?sanitize=true "Testing Powered By SauceLabs")](https://saucelabs.com)

pdf2htmlEX is inspired by the following projects:

* pdftohtml from poppler 
* MuPDF
* PDF.js
* Crocodoc
* Google Doc

#### Special Thanks

* Hongliang Tian
* Wanmin Liu 

pdf2htmlEX的使用方式：

参数说明：

-f,--first-page <int>

说明: 指定要转换的第一页,默认为1。
用法: --first-page 3 表示从第3页开始转换。
-l,--last-page <int>

说明: 指定要转换的最后一页,默认为2147483647(很大的一个数字)。
用法: --last-page 10 表示只转换到第10页。
--zoom <fp>

说明: 指定缩放比例,fp表示浮点数。
用法: --zoom 1.5 将页面放大到1.5倍。
--fit-width <fp>

说明: 将页面宽度缩放到指定的像素宽度。
用法: --fit-width 800 将页面宽度缩放到800像素。
--fit-height <fp>

说明: 将页面高度缩放到指定的像素高度。
用法: --fit-height 600 将页面高度缩放到600像素。
--use-cropbox <int>

说明: 是否使用CropBox而不是MediaBox,默认为1(使用CropBox)。
用法: --use-cropbox 0 表示不使用CropBox。
--dpi <fp>

说明: 指定图形的分辨率(DPI),默认为144。
用法: --dpi 300 将分辨率设置为300dpi。
--embed <string>

说明: 指定哪些元素应嵌入到输出中。
用法: --embed font,javascript 将字体和JavaScript嵌入输出。
--embed-css <int>

说明: 是否将CSS文件嵌入输出,默认为1(嵌入)。
用法: --embed-css 0 表示不嵌入CSS文件。
--embed-font <int>

说明: 是否将字体文件嵌入输出,默认为1(嵌入)。
用法: --embed-font 0 表示不嵌入字体文件。
--embed-image <int>

说明: 是否将图像文件嵌入输出,默认为1(嵌入)。
用法: --embed-image 0 表示不嵌入图像文件。
--embed-javascript <int>

说明: 是否将JavaScript文件嵌入输出,默认为1(嵌入)。
用法: --embed-javascript 0 表示不嵌入JavaScript文件。
--embed-outline <int>

说明: 是否将大纲(目录)嵌入输出,默认为1(嵌入)。
用法: --embed-outline 0 表示不嵌入大纲。
--split-pages <int>

说明: 是否将页面分割为单独的文件,默认为0(不分割)。
用法: --split-pages 1 将每个页面输出为一个单独的文件。
--dest-dir <string>

说明: 指定输出文件的目标目录,默认为当前目录。
用法: --dest-dir /path/to/output 将输出文件保存到指定目录。
--css-filename <string>

说明: 指定生成的CSS文件名,默认为空字符串。
用法: --css-filename styles.css 将CSS文件命名为styles.css。
--page-filename <string>

说明: 当分割页面时,指定页面文件名模板,默认为空字符串。
用法: --page-filename page_{}.html 生成page_1.html,page_2.html等文件。
--outline-filename <string>

说明: 指定生成的大纲文件名,默认为空字符串。
用法: --outline-filename outline.html 将大纲输出到outline.html文件。
--process-nontext <int>

说明: 是否渲染文本以外的图形,默认为1(渲染)。
用法: --process-nontext 0 表示不渲染文本以外的图形。
--process-outline <int>

说明: 是否在HTML中显示大纲,默认为1(显示)。
用法: --process-outline 0 表示不在HTML中显示大纲。
--process-annotation <int>

说明: 是否在HTML中显示注释,默认为0(不显示)。
用法: --process-annotation 1 表示在HTML中显示注释。
--process-form <int>

说明: 是否包含文本字段和单选按钮,默认为0(不包含)。
用法: --process-form 1 表示包含文本字段和单选按钮。
--printing <int>

说明: 是否启用打印支持,默认为1(启用)。
用法: --printing 0 表示禁用打印支持。
--fallback <int>

说明: 是否以回退模式输出,默认为0(不回退)。
用法: --fallback 1 表示以回退模式输出。
--tmp-file-size-limit <int>

说明: 临时文件的最大大小(KB),-1表示无限制,默认为-1。
用法: --tmp-file-size-limit 10240 将临时文件大小限制为10MB。
--embed-external-font <int>

说明: 是否嵌入外部字体的本地匹配,默认为1(嵌入)。
用法: --embed-external-font 0 表示不嵌入外部字体的本地匹配。
--font-format <string>

说明: 嵌入字体文件的后缀(ttf,otf,woff,svg),默认为"woff"。
用法: --font-format ttf 将使用TTF格式嵌入字体。
--decompose-ligature <int>

说明: 是否分解连字符,如fi -> fi,默认为0(不分解)。
用法: --decompose-ligature 1 将分解连字符。
--turn-off-ligatures <int>

说明: 是否明确告诉浏览器不使用连字符,默认为0(不关闭)。
用法: --turn-off-ligatures 1 将明确关闭浏览器的连字符功能。
--auto-hint <int>

说明: 对于没有提示的字体,是否使用fontforge自动提示,默认为0(不使用)。
用法: --auto-hint 1 将对没有提示的字体使用自动提示。
--external-hint-tool <string>

说明: 指定用于字体提示的外部工具(覆盖--auto-hint)。
用法: --external-hint-tool /path/to/tool 使用指定的工具进行字体提示。
--stretch-narrow-glyph <int>

说明: 是否拉伸窄字形而不是填充,默认为0(不拉伸)。
用法: --stretch-narrow-glyph 1 将拉伸窄字形而不是填充。
--squeeze-wide-glyph <int>

说明: 是否压缩宽字形而不是截断,默认为1(压缩)。
用法: --squeeze-wide-glyph 0 将截断宽字形而不是压缩。
--override-fstype <int>

说明: 是否清除TTF/OTF字体的fstype位,默认为0(不清除)。
用法: --override-fstype 1 将清除TTF/OTF字体的fstype位。
--process-type3 <int>

说明: 是否转换Type3字体以供Web使用(实验性),默认为0(不转换)。
用法: --process-type3 1 将尝试转换Type3字体。
--heps <fp>

说明: 合并文本时使用的水平阈值(像素),默认为1。
用法: --heps 2 将水平阈值设置为2像素。
--veps <fp>

说明: 合并文本时使用的垂直阈值(像素),默认为1。
用法: --veps 2 将垂直阈值设置为2像素。
--space-threshold <fp>

说明: 单词断行的阈值(阈值 * 字体em大小),默认为0.125。
用法: --space-threshold 0.2 将单词断行阈值设置为0.2倍字体em大小。
--font-size-multiplier <fp>

说明: 大于1的值可提高渲染精度,默认为4。
用法: --font-size-multiplier 6 将提高渲染精度。
--space-as-offset <int>

说明: 是否将空格字符视为偏移量,默认为0(不视为偏移量)。
用法: --space-as-offset 1 将把空格字符视为偏移量。
--tounicode <int>

说明: 如何处理ToUnicode CMaps(0=自动,1=强制,-1=忽略),默认为0。
用法: --tounicode 1 将强制使用ToUnicode CMaps。
--optimize-text <int>

说明: 是否尝试减少用于文本的HTML元素数量,默认为0(不优化)。
用法: --optimize-text 1 将尝试优化文本的HTML元素数量。
--correct-text-visibility <int>

说明: 文本可见性检查级别,0=不检查,1=完全遮挡的文本,2=部分遮挡的文本,默认为1。
用法: --correct-text-visibility 2 将处理部分遮挡的文本。
--covered-text-dpi <fp>

说明: 如果correct-text-visibility为2且存在部分遮挡文本,则使用该DPI进行渲染,默认为300。
用法: --covered-text-dpi 600 将使用600dpi渲染部分遮挡的文本。
--bg-format <string>

说明: 指定背景图像格式,默认为"png"。
用法: --bg-format jpg 将使用JPG格式作为背景图像。
--svg-node-count-limit <int>

说明: 如果SVG背景图像的节点数超过此限制,则回退到位图背景;负值表示无限制,默认为-1。
用法: --svg-node-count-limit 10000 将SVG节点数限制设置为10000。
--svg-embed-bitmap <int>

说明: 是否将位图嵌入到SVG背景中,0=如果可能则转储到外部文件,默认为1(嵌入)。
用法: --svg-embed-bitmap 0 将位图转储到外部文件(如果可能)。
-o,--owner-password <string>

说明: 指定加密PDF文件的所有者密码。
用法: --owner-password mypassword 使用"mypassword"作为所有者密码。
-u,--user-password <string>

说明: 指定加密PDF文件的用户密码。
用法: --user-password userpass 使用"userpass"作为用户密码。
--no-drm <int>

说明: 是否覆盖文档的DRM设置,默认为0(不覆盖)。
用法: --no-drm 1 将覆盖文档的DRM设置。
--clean-tmp <int>

说明: 是否在转换后删除临时文件,默认为1(删除)。
用法: --clean-tmp 0 将保留临时文件。
--tmp-dir <string>

说明: 指定临时目录的位置,默认为"/tmp"。
用法: --tmp-dir /path/to/tmpdir 将临时文件存储在指定目录。
--data-dir <string>

说明: 指定数据目录,默认为"/usr/local/share/pdf2htmlEX"。
用法: --data-dir /path/to/data 使用指定的数据目录。
--poppler-data-dir <string>

说明: 指定poppler数据目录,默认为"/usr/local/share/pdf2htmlEX/poppler"。
用法: --poppler-data-dir /path/to/poppler 使用指定的poppler数据目录。
--debug <int>

说明: 是否打印调试信



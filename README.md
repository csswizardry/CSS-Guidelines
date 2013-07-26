# CSS 筆記、建議與指導方針總整理

---

在參與大規模、歷時漫長且人手眾多的專案時，所有網頁開發人員都能遵守以下原則極為重要：

+ **維持 CSS 樣式的可維護性 (maintainable)**
+ **維持撰寫風格清晰明瞭並具可讀性 (readable)**
+ **維持 CSS 樣式的延展性 (scalable)**

為了達成上述原則，我們必須使用許多方法才能達成這個目標。

本文第一部分將探討語法、格式與 CSS 剖析；第二部分將從方法論 (approach)、思維框架 (mindframe) 以及撰寫與架構 CSS 的態度著手。

## 內容大綱

* 剖析 CSS 文件
  * 總覽
  * 單一檔案與多檔案
  * 目錄大綱
  * 區段標題
* 樣式載入順序
* 規則解析
* 命名規範
  * JS 鉤子 (JS hooks)
  * I18n
* 註釋
  * 註釋的擴充用法
    * Quasi-qualified selectors
    * 原始碼標籤
    * 繼承標記 (Object/extension pointers)
* 撰寫 CSS
* 建構新組件 (Building new components)
* 物件導向 CSS (OOCSS)
* 版面配置
* UI 尺寸
  * 字級大小
* 簡寫
* IDs
* 選取器
  * 過修飾選取器
  * 選取器性能
* 選取器繼承
* `!important`
* 魔數與絕對比例
* 條件式註解
* 偵錯(Debugging)
* 前置處理器

註：ID 不能包含漢字，所以在 Github Markdown 中暫時無法實現跳轉。

---

## 剖析 CSS 文件

無論撰寫什麼文件，我們都應當盡力維持統一的風格，包括統一的註釋、統一的語法與統一的命名規範。

### 總則

盡量將行寬控制在 80 字元以下。漸變（gradient）相關的語法以及註釋中的 URL 等可以當作例外，畢竟這部分我們也無能為力。

我傾向於用 4 個空格而非 Tab 縮排，並且將不同的樣式拆分成多行。

### 單一檔案與多檔案

有些人喜歡將樣式寫成一個大文件，這並不賴，而且如果你按照下文的規則來撰寫的話也不會遇到什麼問題。我在遷移至 Sass 之後，開始將樣式拆分成眾多小文件。這也不賴。無論你採用什麼方式，下文中的規則都將適用。這兩種寫法僅僅在目錄以及區段標題上有所差異。

### 目錄大綱

在 CSS 的開頭，我會寫一份目錄，例如：

    /*------------------------------------*\
        $CONTENTS
    \*------------------------------------*/
    /**
     * CONTENTS............You』re reading it!
     * RESET...............Set our reset defaults
     * FONT-FACE...........Import brand font files
     */

這份目錄可以告訴其他網頁開發人員這個文件中具體含有哪些內容。這份目錄中的每一項都與其對應的區段標題相同。

如果你在維護一份規模較大的單文件 CSS，對應的區塊將也在同一文件中。如果你是在撰寫一組小文件，那麼目錄中的每一項應當對應相應的 @include 語句。

### 區段標題

目錄應當對應區塊的標題。請看如下範例：

    /*------------------------------------*\
        $RESET
    \*------------------------------------*/

區段標題前綴 `$` 可以讓我們使用（[Cmd|Ctrl]+F）命令查找 `$[SECTION-NAME]`，同時 **將搜尋範圍限制在區段標題中**。

如果你在維護一份大文件，那麼在區塊之間空 5 行，如下：

    /*------------------------------------*\
        $RESET
    \*------------------------------------*/
    [Our
    reset
    styles]
    
    
    
    
    
    /*------------------------------------*\
        $FONT-FACE
    \*------------------------------------*/

在大文件中快速翻動時這些大塊的空檔有助於區分區塊。

如果你在維護多份、以 @include 連接的 CSS 的話，在每份文件頭加上標題即可，不必這樣空行。

## 樣式載入順序

盡量按照特定順序撰寫樣式規則，這將確保你充分發揮 CSS 縮寫中第一個 <i>C</i> 的意義：Cascade，串聯。

一份規劃良好的 CSS 應當按照如下順序載入或撰寫：

1. **Reset** 重置所有樣式為 0
2. **元素類型** 沒有設定 class 的 `h1`、`ul` 等元素，也就是元素的預設樣式
3. **物件以及抽像內容** 最一般、最基礎的設計模式
4. **元件** 從物件組合而成的完整元件
5. **修補** 針對異常狀態

如此一來，當你依次撰寫 CSS 時，每個區塊都可以自動繼承在它之前區塊的屬性。這樣就可以減少原始碼相互抵消的部分，減少某些特殊的問題，構成設計更理想的 CSS 結構。

關於這方面的更多信息，強烈推薦 Jonathan Snook 的 [SMACSS](http://smacss.com)。

## CSS 規則集分析

    [selector]{
        [property]:[value];
        [<- Declaration ->]
    }

    [選取器]{
        [屬性]:[值];
        [<- 其他樣式 ->]
    }

撰寫 CSS 樣式時，我習慣遵守這些規則：

* class 名稱以連字符（-）連接，除了下文提到的 BEM 命名法；
* 縮排 4 空格；
* 將不同的樣式拆分成多行；
* 不同的樣式以相關性順序排列，而非字母順序；
* 有前綴的樣式適當縮排，對齊其值；
* 縮排樣式從而反映 DOM；
* 保留最後一條樣式規則結尾的分號。

例如：

    .widget{
        padding:10px;
        border:1px solid #BADA55;
        background-color:#C0FFEE;
        -webkit-border-radius:4px;
           -moz-border-radius:4px;
                border-radius:4px;
    }
        .widget-heading{
            font-size:1.5rem;
            line-height:1;
            font-weight:bold;
            color:#BADA55;
            margin-right:-10px;
            margin-left: -10px;
            padding:0.25em;
        }

我們可以發現，`.widget-heading` 是 `.widget` 的子元素，因為前者比後者多縮排了一級。這使得網頁開發人員在閱讀這些樣式時可以快速獲取信息。

我們還可以發現 `.widget-heading` 的樣式是根據其相關性排列的：`.widget-heading` 是文字元素，所以我們先新增字體相關的樣式，接下來是其它的。

以下是一個沒有拆分成多行的例子：

    .t10    { width:10% }
    .t20    { width:20% }
    .t25    { width:25% }       /* 1/4 */
    .t30    { width:30% }
    .t33    { width:33.333% }   /* 1/3 */
    .t40    { width:40% }
    .t50    { width:50% }       /* 1/2 */
    .t60    { width:60% }
    .t66    { width:66.666% }   /* 2/3 */
    .t70    { width:70% }
    .t75    { width:75% }       /* 3/4*/
    .t80    { width:80% }
    .t90    { width:90% }

在這個例子（來自[inuit.css』s table grid system](https://github.com/csswizardry/inuit.css/blob/master/inuit.css/partials/base/_tables.scss#L88)）中，將 CSS 放在一行內可以使得原始碼更緊湊。

## 命名規範

一般情況下我都是以連字符（-）連接 class 的名字（例如 `.foo-bar` 而非 `.foo_bar` 或 `.fooBar`），不過在某些特定的時候我會用 BEM（Block, Element, Modifier）命名法。

<abbr title="Block, Element, Modifier">BEM</abbr> 命名法可以使得選取器更規範，更清晰，更具語意。

該命名法按照如下格式：

    .block{}
    .block__element{}
    .block--modifier{}

其中：

* `.block` 代表某個基本的抽像元素；
* `.block__element` 代表 `.block` 這一整體的一個子元素；
* `.block--modifier` 代表 `.block` 的某個不同狀態。

打個比方：

    .person{}
    .person--woman{}
        .person__hand{}
        .person__hand--left{}
        .person__hand--right{}

這個例子中我們描述的最基本元素是一個人，然後這個人可能是一個女人。我們還知道人擁有手，這些是人體的一部分，而手也有不同的狀態，如同左手與右手。

這樣我們就可以根據親元素來規定選取器的命名空間並傳達該選取器的職能，它是一個子元素（`__`）還是不同狀態（`--`）？

由此，`.page-wrapper` 是一個獨立的選取器。這是一個符合規範的命名，因為它不是其它元素的子元素或其它狀態；然而 `.widget-heading` 則與其它對像有關聯，它應當是 `.widget` 的子元素，所以我們應當將其重命名為 `.widget__heading`。

BEM 命名法雖然不太好看，而且相當冗長，但是它使得我們可以透過名稱快速得知元素的功能和元素之間的關係。與此同時，BEM 語法中的重複部分非常有利於 gzip 的壓縮演算法。

無論你是否使用 BEM 命名法，你都應當確保 class 命名得當，力保一字不多、一字不少；將元素命名抽像化以提高重複使用性（例如 `.ui-list`，`.media`）。由此延伸出去的元素命名則要盡量精準（例如 `.user-avatar-link`）。不用擔心 class 名的數量或長度，因為寫得好的原始碼 gzip 也能有效壓縮。

### HTML 中的 class

為了確保易讀性，在 HTML 標記中用兩個空格隔開 class 名，例如：

    <div class="foo--bar  bar__baz">

增加的空格應當可以使得在使用多個 class 時更易閱讀與定位。

### JS 鉤子 (JS hooks)

**千萬不要把 CSS 樣式用作 JavaScript 鉤子。**把 JS 行為與樣式混在一起將無法對其分別處理。

如果你要把 JS 和某些標記綁定起來的話，寫一個 JS 專用的 class。簡單地說就是劃定一個前綴 `.js-` 的命名空間，例如 `.js-toggle`，`.js-drag-and-drop`。這意味著我們可以透過 class 同時綁定 JS 和 CSS 而不會因為衝突而引發麻煩。

    <th class="is-sortable  js-is-sortable">
    </th>

上面的這個標記有兩個 class，你可以用其中一個來給這個可排序的表格欄新增樣式，用另一個新增排序功能。

### I18n

雖然我（該 CSS Guideline 文件原作者 Harry Roberts）是個英國人，而且我一向拼寫 <i>colour</i> 而非 <i>color</i>，但是為了統一性，我認為在 CSS 中用美式拼法更佳。CSS 以及其它多數語言都是以美式拼法撰寫，所以如果在 `.colour-picker{}` 中寫 `color:red` 就缺乏統一性。我以前主張同時用兩種拼法，例如：

    .color-picker,
    .colour-picker{
    }

但是我最近參與了一份規模龐大的 Sass 專案，這個專案中有許多的顏色變量（例如 `$brand-color`，`$highlight-color` 等等），每個變量要維護兩種拼法實在辛苦，要查找並替換時也需要兩倍的工作量。

所以為了統一性，把所有的 class 與變量都以你參與的專案的慣用拼法命名即可。

## 註釋

我使用行寬不超過 80 字元的塊狀註釋：

    /**
     * This is a docBlock style comment
     * 
     * This is a longer description of the comment, describing the code in more
     * detail. We limit these lines to a maximum of 80 characters in length.
     * 
     * We can have markup in the comments, and are encouraged to do so:
     * 
       <div class=foo>
           <p>Lorem</p>
       </div>
     * 
     * We do not prefix lines of code with an asterisk as to do so would inhibit
     * copy and paste.
     */


    /**
     * 這是一個文件塊（DocBlock）風格的註釋。
     *
     * 這裡開始是描述更詳細、篇幅更長的註釋正文。當然，我們要把行寬控制在 80 字以內。
     *
     * 我們可以在註釋中嵌入 HTML 標記，而且這也是個不錯的辦法：
     *
        <div class=foo>
            <p>Lorem</p>
        </div>
     *
     * 如果是註釋內嵌的標記的話，在它前面不加星號，否則會被複製進去。
     */

在註釋中應當盡量詳細描述原始碼，因為對你來說清晰易懂的內容對其他人可能並非如此。每寫一部分原始碼就要專門寫註釋以詳解。

### 註釋的擴充用法

註釋有許多很先進的用法，例如：

* Quasi-qualified selectors
* 原始碼標籤 (Tagging code)
* 繼承標記 (Object/extension pointers)

#### Quasi-qualified selectors

你應當避免過分修飾選取器，例如如果你能寫 `.nav{}` 就盡量不要寫 `ul.nav{}`。過分修飾選取器將影響性能，影響 class 重複使用性，增加選取器私有度。這些都是你應當竭力避免的。

不過有時你可能希望告訴其他網頁開發人員 class 的使用範圍。以 `.product-page` 為例，這個 class 看起來像是一個根容器，可能是 `html` 或者 `body` 元素，但是僅憑 `.product-page` 則無法判斷。

我們可以在選取器前加上准修飾（即將前面的類型選取器註釋掉）來描述我們規劃的 class 作用範圍：

    /*html*/.product-page{}

這樣我們就能準確得知該 class 的作用範圍而不會影響重複使用性。

其它例子如：

    /*ol*/.breadcrumb{}
    /*p*/.intro{}
    /*ul*/.image-thumbs{}

這樣我們就能在不影響原始碼私有度的前提下得知 class 作用範圍。

#### 原始碼標籤

如果你寫了一個新規則的話，可以在它上面加上標籤，例如：

    /**
     * ^navigation ^lists
     */
    .nav{}
    
    /**
     * ^grids ^lists ^tables
     */
    .matrix{}

這些標籤可以使得其他網頁開發人員快速找到相關原始碼。如果一個網頁開發人員需要查找和列表相關的部分，他只要搜尋 `^lists` 就能快速定位到 `.nav`，`.matrix` 以及其它相關部分。

#### 繼承標記 (Object/extension pointers)

將物件導向的思路用於 CSS 撰寫的話，你經常能找到兩個部分與 CSS 密切相關（其一為骨架，其一為擴充）卻分列兩處。我們可以用繼承標記來在原元素和繼承元素之間建立緊密聯繫。這些在註釋中的寫法如下：

在元素的基底樣式中：

    /**
     * Extend `.foo` in theme.css
     */
     .foo{}

在元素的擴充樣式中：

    /**
     * Extends `.foo` in base.css
     */
     .bar{}

這樣一來我們就能在兩塊相隔很遠的原始碼間建立緊密聯繫。

---

## 撰寫 CSS

之前的章節主要探討如何規劃 CSS，這些都是易於量化的規則。本章將探討更理論化的東西，也將探討我們的態度與方法。

## 建構新組件 (Building new components)

建構新組件時，要在著手處理 CSS **之前** 寫好 HTML 部分。這可以令你準確判斷哪些 CSS 屬性可以繼承，避免重複浪費。

先寫標記的話，你就可以關注資料、內容與語意，在這之後再新增需要的 class 和 CSS 樣式。

## 物件導向 CSS (OOCSS)

我以物件導向 CSS 的方式寫原始碼。我把組件分成結構（對像）與外觀（擴充）。正如以下分析（注意這個只是筆記而非例子）：

    .room{}
    
    .room--kitchen{}
    .room--bedroom{}
    .room--bathroom{}

我們在屋子裡有許多房間，它們都有共同的特點：它們都包含地板、天花板、牆壁和門。這些共享的部分我們可以放到一個抽像的 `.room{}` class 中。不過我們還有其它與眾不同的房間：一個廚房可能有地磚，臥室可能有地毯，洗手間可能沒有窗戶但是臥室會有，每個房間的牆壁顏色也許也會不一樣。物件導向 CSS 的思路使得我們把相同部分抽像出來組成結構部分，然後用更具體的 class 來擴充這些特徵並新增特殊的處理方法。

所以比起撰寫大量的特殊區塊，應當努力找出這些區塊中重複的設計模式並將其抽取出來，寫成一個可以重複使用的 class，將其用作基礎然後撰寫其它擴充區塊的特殊情形。

當你要撰寫一個新組件時，將其拆分成結構和外觀。撰寫結構部分時用最通用 class 以保證重複使用性，撰寫外觀時用更具體的 class 來新增設計方法。

## 版面配置

所有組件都不應該定義寬度，保持其流動(fluid)的特性，而由其上層元素或網格系統來決定其寬度。

**永遠不要** 宣告高度。高度應當僅僅用於尺寸已經固定的東西，例如圖片和 CSS Sprite。在 `p`，`ul`，`div` 等元素上不應當定義高度。如果需要的話可以寫 `line-height`，這個更加靈活。

網格系統應當當作書架來理解。是它們容納內容，而不是把它們本身當成內容裝起來，正如你先搭起書架再把東西放進去。比起定義它們的尺寸，把網格系統和元素的其它屬性分來開處理更有助於版面配置，也使得我們的前端工作更有效率。

你在網格系統上不應當新增任何樣式，他們僅僅是為版面配置而用。在網格系統內部再新增樣式。在網格系統中任何情況下都不要新增盒模型相關屬性。

## UI 尺寸

我用很多方法設定 UI 尺寸，包括百分比，`px`，`em`，`rem` 以及乾脆什麼都不用。

理想情況下，網格系統應當用百分比設定。如上所述，因為我用網格系統來固定欄寬和頁寬，所以我可以不用理會元素的尺寸。

我用 rem 定義字級大小，並且以 px 輔助下相容於舊版瀏覽器。這可以兼具 em 和 px 的優勢。下面是一個非常漂亮的 Sass Mixin，假設你在別處定義了基本字級大小（base-font-size）的話，用它就可以產生 rem 以及相容於舊版瀏覽器的 px。

    @mixin font-size($font-size){
        font-size:$font-size +px;
        font-size:$font-size / $base-font-size +rem;
    }

我只在已經固定尺寸的元素上使用 px，包括圖片以及尺寸已經用 px 固定的 CSS Sprite。

### 字級大小

我會定義一些與網格系統原理類似的 class 來定義字級大小。這些 class 可以用於雙重標題分級 (These classes can be used to style type in a double stranded heading hierarchy.)，關於這點請閱讀 [Pragmatic, practical font-sizing in CSS](http://csswizardry.com/2012/02/pragmatic-practical-font-sizing-in-css)。

## 簡寫

**CSS 簡寫應當謹慎使用。**
    
撰寫像 `background:red;` 這樣的屬性的確很省事，但是你這麼寫的意思其實是同時聲明 `background-image:none; background-position:top left; background-repeat: repeat; background-color:red;`。雖然大多數時候這樣不會出什麼問題，但是哪怕只出一次問題就值得考慮要不要放棄簡寫了。這裡應當將其改為 `background-color:red;`。

類似的，像 `margin:0;` 這樣的聲明的確簡潔清爽，但是還是應當 **盡量寫清楚**。如果你只是想修改底邊的 `margin`，最好具體一些，寫成 `margin-bottom:0;`。

反過來，你需要聲明的屬性也要寫清楚，不要因為簡寫而波及其它屬性。例如如果你只想改掉底部的 `margin`，那就不要用會把其它邊距也清零的 `margin:0`。

簡寫雖然是好東西，但是注意切勿濫用。

## ID

在我們開始處理選取器之前，牢記這句話：

**在 CSS 裡堅決不要用 ID。**

在 HTML 裡 ID 可以用於 JS 以及錨點定位，但是在 CSS 裡只要用 class，一個 ID 也不要用。

Class 的優勢在於重複使用性，而且私有度也並不高。私有度非常容易導致問題，所以將其降低就尤為重要。ID 的私有度是 class 的 **255** 倍，所以在 CSS 中堅決不要使用。

##  選取器

務必維持選取器簡短且有效率。

透過頁面元素位置而定位的選取器並不理想。例如 `.sidebar h3 span{}` 這樣的選取器就是定位過於依賴相對位置，所以很難把 span 移到 h3 和 sidebar 外面並維持其樣式。

結構複雜的選取器將會影響性能。選取器結構越複雜（如 `.sidebar h3 span` 為三層，`.content ul p a` 是四層），瀏覽器的消耗就越大。

盡量使得樣式不依賴於其定位，盡量維持選取器簡潔清晰。

作為一個整體，選取器應當盡量簡短（例如只有一層結構），但是 class 名則不應當過於簡略，例如 `.user-avatar` 就遠比 `.usr-avt` 好。

**牢記：** class 無所謂是否語意化；應當關注它們是否合理。不要強調 class 名要符合語意，而要注重使用合理且不會過時的名稱。

### 過度修飾的選取器

由前文所述，過度修飾的選取器並不理想。

過度修飾的選取器是指像 `div.promo` 這樣的。很可能你只用 `.promo` 也能得到相同的效果。當然你可能偶爾會需要用元素類型來修飾 class（例如你寫了一個 `.error` 而且想讓它在不同的元素類型中顯示效果不一樣，例如 `.error{ color:red; }` `div.error{ padding:14px;}`），但是大多數時候還是應當盡量避免。

再舉一個修飾過度的選取器例子，`ul.nav li a{}`。如前文所說，我們馬上就可以刪掉 `ul` 因為我們知道 `.nav` 是個列表，然後我們就可以發現 `a` 一定在 `li` 中，所以我們就能將這個選取器改寫成 `.nav a{}`。

### 選取器性能

雖然瀏覽器性能日漸提升，渲染 CSS 速度越來越快，但是你還是應當關注效率。使用間斷、沒有嵌套的選取器，不把全局選取器（`*{}`）用作核心選取器，避免使用日漸複雜的 CSS3 新選取器可以避免這樣的問題。

譯注，核心選取器：瀏覽器解析選取器為從右向左的順序，最右端的元素是樣式生效的元素，是為核心選取器。

## 使用 CSS 選取器的目的

比起努力運用選取器定位到某元素，更好的辦法是直接給你想要新增樣式的元素直接新增一個 class。我們以 `.header ul{}` 這樣一個選取器為例。

假定這個 `ul` 就是這個網站的全站導航，它位於 header 中，而且目前為止是 header 中唯一的 `ul` 元素。`.header ul{}` 的確可以生效，但是這樣並不是好方法，它很容易過時，而且非常晦澀。如果我們在 header 中再新增一個 `ul` 的話，它就會套用我們給這個導航部分寫的樣式，哪怕我們設想的不是這個效果。這意味著我們要麼要重構許多原始碼，要麼給後面的 `ul` 新寫許多樣式來抵消之前的影響。

你的選取器必須符合你要給這個元素新增樣式的原因。思考一下， **「我定位到這個元素，是因為它是 `.header` 下的 `ul`，還是因為它是我的網站導航？」**這將決定你應當如何使用選取器。

確保你的核心選取器不是類型選取器，也不是高級對像或抽像選取器。例如你在我們的 CSS 中肯定找不到諸如 `.sidebar ul{}` 或者 `.footer .media{}` 這樣的選取器。

表達清晰：直接找到你要新增樣式的元素，而非其親元素。不要想當然地認為 HTML 不會改變。 **用 CSS 直接命中你需要的元素，而非投機取巧。**

完整內容請參考我的文章 [Shoot to kill; CSS selector intent](http://csswizardry.com/2012/07/shoot-to-kill-css-selector-intent/)

## `!important`

只在起輔助作用的 class 上用 `!important`。用 `!important` 提升優先級也可以，例如如果你要讓某條規則 **一直** 生效的話，可以用 `.error{ color:red!important; }`。

避免主動使用 `!important`。例如 CSS 寫得很複雜時不要用它來取巧，要好好整理並重構之前的部分，維持選取器簡短並且避免用 ID 將效果拔群。

## 魔數與絕對定位

魔數（Magic Number）是指那些「剛好有效果」的數字，這東西非常不好，因為它們只是治標不治本而且缺乏延展性。

例如 `.dropdown-nav li:hover ul{ top:37px; }` 把下拉菜單移動下來遠非良策，因為這裡的 37px 就是個魔數。37px 會生效的原因是因為這時 `.dropbox-nav` 碰巧高 37px 而已。

這時你應該用 `.dropdown-nav li:hover ul{ top:100%; }`，也即無論 `.dropbox-down` 多高，這個下拉菜單都會往下移動 100%。

每當你要在原始碼中放入數字的時候，請三思而後行。如果你能用一個關鍵字（例如  `top:100%` 意即「從上面拉到最下面」）替換之，或者有更好的解決方法的話，就盡量避免直接出現數字。

你在 CSS 中留下的每一個數字，都是你許下而不願遵守的承諾。

## 條件式註解

專門為 IE 寫的樣式基本上都是可以避免的，唯一需要為 IE 專門處理的是為了處理舊版 IE 不支援的內容（例如 PNG）。

簡而言之，如果你重構 CSS 的話，所有的版面配置和盒模型都不用額外相容於 IE。也就是說你基本上不用 `<!--[if IE 7]> element{ margin-left:-9px; } < ![endif]-->` 或者類似的相容於 IE 的寫法。 

## 偵錯(Debugging)

如果你要解決 CSS 問題的話， **先把舊原始碼拿掉再寫新的** 。如果舊的 CSS 中有問題的話，寫新原始碼是解決不了的。

把 CSS 原始碼和 HTML 部分刪掉，直到沒有 BUG 為止，然後你就知道問題出在哪裡了。

有時候寫上一個 `overflow:hidden` 或者其它能把問題藏起來的原始碼的確效果立竿見影，但是 overflow 方面可能根本就沒問題。所以 **要治本，而不是單純治標**。

## 前置處理器

我用 Sass。使用時應當 **靈活運用** 。用 Sass 可以令你的 CSS 更強大，但是不要嵌套得太複雜。在 Vanilla CSS 中，只在必要的地方用嵌套即可，例如：

    .header{}
    .header .site-nav{}
    .header .site-nav li{}
    .header .site-nav li a{}

這樣的寫法在普通 CSS 裡完全用不到。以下為 **不好的** Sass 寫法：

    .header{
        .site-nav{
            li{
                a{}
            }
        }
    }

如果你用 Sass 的話，盡量這麼寫：

    .header{}
    .site-nav{
        li{}
        a{}
    }

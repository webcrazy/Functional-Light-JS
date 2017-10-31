# Functional-Light JavaScript
# Chapter 1: Why Functional Programming?

> Functional programmer: (noun) One who names variables "x", names functions "f", and names code patterns "zygohistomorphic prepromorphism"
>
> James Iry ‏@jamesiry 5/13/15
>
> https://twitter.com/jamesiry/status/598547781515485184

Functional Programming (FP) ဆိုတာ အယူအဆ အသစ်တစ်ခုတော့လုံးဝ မဟုတ်ပါဘူး။ Programming စကတည်းကရှိနေခဲ့တာပါ။ အခုလိုပြောရင် မျှတပါ့မလား မသိပေမယ့်၊  လွန်ခဲ့တဲ့ နှစ်အနည်းငယ်မတိုင်ခင် အထိ developer နယ်ပယ်မှာ ရေပန်းစားတဲ့ အယူအဆတစ်ခု မဟုတ်ခဲ့တာတော့ သေချာပါတယ်။ FP ဟာ သင်ကြားရေးနယ်ပယ်မှာ ပိုနာမည်ကြီးတယ်လို့ကျနော်ထင်ပါတယ်။

ဒါပေမယ့် အဲ့ဒါတွေ အကုန်လုံးက စိန်ခေါ်မှုတွေပါပဲ။ FP နဲ့ ပတ်သက်ပြီး စိတ်ဝင်စားမှု မြင့်တက်လာတာက languages အဆင့်သာမကပဲ libraries တွေ frameworks တွေအထိပါပဲ။သင်အခုဒီစာကိုဖတ်နေတာကလည်း FB ဆိုတာ လှစ်လျူရှုထားလို့ မရတော့ဘူးလို့ သင်သဘောပေါက်လို့လဲ ဖြစ်ကောင်းဖြစ်မှာပါ။ ဒါမှ မဟုတ်သင်ဟာ ကျနော့်လိုပဲ FP ကို အရင်က အကြိမ်ပေါင်းများစွာကြိုးစားဖူးပေမယ့် အခေါ်အဝေါ်တွေ သင်္ချာ အသုံးအနှုန်းတွေကြားမှာ ရုန်းကန်နေရတာလည်း ဖြစ်နိုင်ပါတယ်။ 

ပထမ သင်ခန်းစာရဲ့ ရည်ရွယ်ချက်က "ဘာလို့ ငါ့ရဲ့ code တွေကို FP စတိုင်သုံးရမှာလဲ" နဲ့ "Javascript ရဲ့ FP နဲ့ တခြား FP ကို ဘယ်လိုနှိုင်းယှဉ်မှာလဲ" ဆိုတဲ့ မေးခွန်းလိုမျိုးတွေကို ရှင်းပြဖို့ လိုအပ်တာ လုပ်သွားမှာဖြစ်ပါတယ်။ Chapter 2 ကနေစပြီး စာအုပ်ပြီးတဲ့ အထိ JS ကို functional lite ပုံစံမျိုး ဘယ်လိုရေးမလဲဆိုတာ တစ်ပိုင်းတစ်ပိုင်း ရှင်းပြသွားမှာပါ။

## At A Glance
Functional-Lite Javascript ရဲ့ သဘောကို before-and-after code နဲ့ အတိုချုပ်သရုပ်ပြကြည့်ရအောင်။ စဉ်းစားကြည့်ပါ။

```js
var numbers = [4,10,0,27,42,17,15,-6,58];
var faves = [];
var magicNumber = 0;

pickFavoriteNumbers();
calculateMagicNumber();
outputMsg();                // The magic number is: 42

// ***************

function calculateMagicNumber() {
    for (let fave of faves) {
        magicNumber = magicNumber + fave;
    }
}

function pickFavoriteNumbers() {
    for (let num of numbers) {
        if (num >= 10 && num <= 20) {
            faves.push( num );
        }
    }
}

function outputMsg() {
    var msg = `The magic number is: ${magicNumber}`;
    console.log( msg );
}
```
အခု အဖြေတော့ အတူတူပဲ၊ မတူတဲ့ ပုံစံ တစ်ခုကို စဉ်းစားကြည့်ပါ။

```js
var sumOnlyFavorites = FP.compose( [
    FP.filterReducer( FP.gte( 10 ) ),
    FP.filterReducer( FP.lte( 20 ) )
] )( sum );

var printMagicNumber = FP.pipe( [
    FP.reduce( sumOnlyFavorites, 0 ),
    constructMsg,
    console.log
] );

var numbers = [4,10,0,27,42,17,15,-6,58];

printMagicNumber( numbers );        // The magic number is: 42

// ***************

function sum(x,y) { return x + y; }
function constructMsg(v) { return `The magic number is: ${v}`; }
```
FP နဲ့ Functional-Light ကိုသင်နားလည်ပြီဆိုရင် ဒုတိယ စာပိုဒ်ကို ဖတ်ပြီး  စိတ်ထဲကနေ နားလည်အောင်ကြိုးစားတဲ့အခါ ဒါမျိုးဖြစ်ကောင်းဖြစ်ပါလိမ့်မယ်။

> ကျနော်တို့ functions သုံးခုပေါင်းထားတဲ့ `sumOnlyFavourites(..)`function တစ်ခုကို တည်ဆောက်ပါ့မယ်။ value တစ်ခုက 10 (သို့) 10 ထက်ကြီးလား စစ်တဲ့ filter နှင့် 20 သို့ 20 ထက်ငယ်လား စစ်တဲ့ filter နှစ်ခုကို ပေါင်းစပ်ပါ့မယ်။
> နောက်ပြီး transducer composition မှာ `sum(..)` reducer ကို ပေါင်းထည့်ပါ့မယ်။ ရလာတဲ့ `sumOnlyFavourites(..)` က ထည့်လိုက်တဲ့ value တစ်ခုက filters နှစ်ခုစလုံးကို pass လား၊ pass တယ်ဆိုရင် accumulator value ထဲကို ပေါင်းထည့်တဲ့ reducer function တစ်ခုဖြစ်ပါတယ်။
> 
> Then we make another function called `printMagicNumber(..)` which first reduces a list of numbers using that `sumOnlyFavorites(..)` reducer we just defined, resulting in a sum of only numbers that passed the *favorite* checks. Then `printMagicNumber(..)` pipes that final sum into `constructMsg(..)`, which creates a string value that finally goes into `console.log(..)`.
> နောက်ပြီး `printMagicNumber(..)`လို့ခေါ်တဲ့ function တစ်ခုပြုလုပ်ပါမယ်။ အဲ့ဒီ function က `sumOnlyFavourites(..)` သုံးပြီး numbers list ကို ပထမဆုံး reduce လုပ်မယ်။ "favourite" check ကို pass လာတဲ့ numbers တွေပဲ ပေါင်းထားတာရလာမယ်။ နောက်ပြီး `printMagicNumber(..)`ကနေ နောက်ဆုံး ပေါင်းလဒ်ကို `constructMsg(..)`ထဲထည့်ပေးပြီး ရလာတဲ့ string value ကို နောက်ဆုံး `console.log(..)`
> 
All those moving pieces *speak* to an FP developer in ways that likely seem highly unfamiliar to you right now. This book will help you *speak* that same kind of reasoning so that it's as readable to you as any other code, if not more so!

အခု code နှိုင်းယှဉ်မှုနှင့်ပတ်သတ်ပြီး မှတ်ချက်အချို့၊

* စာဖတ်သူတော်တော်များများအတွက် အရင် snippet က နောက်ပိုင်း snippet ထက် ပိုပြီး သက်သာမယ်၊ ဖတ်ရအဆင်ပြေမယ်၊ ထိန်းသိမ်းရ လွယ်ကူမယ်လို့ ခံစားရနိုင်ပါတယ်။ အဲ့ဒီလိုထင်ရင်လည်း လုံဝ အဆင်ပြေပါတယ်။ သင်မှန်ပါတယ်။ သင်ဟာ စာအုပ်တစ်ခုလုံး အဆုံးအထိဖတ်မယ်၊ ဆွေးနွေးတဲ့ အကြောင်းအရာတွေအကုန် လေ့ကျင့်မယ် ဆိုရင် ဒုတိယ snippet က တစ်ခါတလေ ပိုပြီး သဘာဝ ကျမယ်၊ ပိုပြီးတော့တောင် သုံးသင့်မယ်လို့ ယုံကြည်ပါတယ်။

* သင်ဟာ အပေါ်က နှစ်ခုစလုံးနဲ့ မတူပဲ လုံဝ ကွဲပြားခြားနားပြီး ကောင်းမွန်တဲ့ ပုံစံနဲ့ task တွေကို ဖြေရှင်းခဲ့တာလည်းဖြစ်နိုင်ပါတယ်။ အဲ့လိုဆိုလည်း အဆင်ပြေပါတယ်။ ဒီစာအုပ်ဟာ ဒီနည်းအတိုင်း ဒီလိုပဲလုပ်ပါလို့ ပြောမှာ မဟုတ်ပါဘူး။ ရည်ရွယ်ချက်က မတူတဲ့ patterns တွေရဲ့ ကောင်းကွက်၊ဆိုးကွက်တွေကို သရုပ်ပြပြီး သင့်ကိုမှန်ကန်တဲ့ ဆုံဖြတ်ချက်တွေချနိုင်အောင်ပါ။ ဒီစာအုပ်ဖတ်လို့ပြီးရင် ပုဒ်စာ တစ်ခုကို ဖြေရှင်းဖို့ ချည်းကပ်တဲ့အခါ ဒုတိယ snippet နဲ့ ပိုရင်းနီးမှာပါ။

* သင့်အတွက် အသုံးဝင်တဲ့ ဖတ်စရာ တစ်ခုခုများရှိမလားလို့ စာအုပ်အစမှာ ရှာဖွေနေတဲ့ အတွေ့အကြုံရှိပြီးသား FP developer လည်း ဖြစ်နိုင်ပါတယ်။ ဒုတိယ snippet မှာ ရင်းနှီးပြီးသား အစိတ်အပိုင်းတွေ အသေအချာ ရှိပါတယ်။ ငါဆိုရင်တော့ အဲ့လိုလုပ်ခဲ့မှာ မဟုတ်ဘူးလို့ မကြခဏ တွေးနေမယ်လို့လည်း လောင်းပါတယ်။ အဲ့လိုတွေးတာလည်း အဆင်ပြေပြီး ဆီလျော်ပါတယ်။

  အခုစာအုပ်ဟာ သမရိုးကျ FB စာအုပ် မဟုတ်ပါဘူး။ We'll at times seem quite heretical in our approaches. We're seeking to strike a pragmatic balance between the clear undeniable benefits of FP, and the need to ship workable, maintainable JS without having to tackle a daunting mountain of math/notation/terminology. ဒါဟာ သင့်ရဲ့ FP မဟုတ်ပါဘူး။ "Functional-Lite JavaScript" ပဲဖြစ်ပါတယ်။

ဒီစာအုပ်ကို ဘယ်လို အကြောင်းကြောင့်ပဲဖတ်ဖတ် ကြိုဆိုပါတယ်။

## Confidence

 JavasScript သုံးပြီး software developer ဆရာအဖြစ် အလုပ်လုပ်ရင်း ကျနော့မှာ အလွန်ရိုးရှင်းတဲ့ ယူဆချက်ရှိပါတယ်။ အဲ့ဒါက သင်ယုံလို့မရတဲ့ code က သင်နားမလည်တဲ့ code ပါပဲ။ ပြောင်းပြန်ဆိုလည်းမှန်ပါတယ်။ သင်နားမလည်တဲ့ code ဟာ သင် ယုံလို့ မရတဲ့ code ပါပဲ။ နောက်ပြီး သင့် code ကို ယုံလို့မရဘူး နားမလည်ဘူးဆိုရင် သင့်ရဲ့ code ဟာ ပြသနာအတွက် သင့်တော်တယ်လို့ ယုံကြည်ချက် မရနိုင်ပါဘူး။ သင့်ရဲ့ program ကို run ကြည့်ပြီး ကံကောင်းပါစေဆုတောင်းရမှာပါ။

ဒီနေရာမှာ ယုံကြည်မှုဆိုတာ သင်က သင့် code ကို run ကြည့်မှ မဟုတ်ပဲ ဖတ်ကြည့်ပြီးဖြစ်ဖြစ် စဉ်းစားပြီးဖြစ်ဖြစ် ဒီ code ဟာ ဘာလုပ်သင့်တယ် မဟုတ်ပဲ၊ ဒီလိုအလုပ်လုပ်ရမယ်လို့ အသေအချာသိတာကိုပြောတာပါ။
 
ဖြစ်နိုင်ခြေက ကျနော်တို့က ကျနော်တို့ program တွေရဲ့ မှန်ကန်မှုကို test suites တွေ run လို့ရတဲ့ အဖြေပေါ်မှာ မှီခိုလေ့ ရှိပါတယ်။ tests တွေက မကောင်းဘူး လို့ မဆိုလိုပါဘူး။ ဒါပေမယ့် test suite တွေ မ run ကြည့်ခင် ဒီ test suite တွေ pass မယ်လို့ ကိုယ့် code ကိုယ် ကောင်းကောင်း နားလည်သင့်ပါတယ်။ 

FP ရဲ့ အခြေခံ နည်းစနစ်က ကိုယ့်ရဲ့ program ကို ဖတ်ကြည့်ယုံနဲ့ ယုံကြည်မှုရှိရမယ်ဆိုတဲ့ အပေါ်မှာ ဖွဲ့စည်းထားတာပါ။ ကိုယ့်ရဲ့ program မှာသုံးဖို့ FP ကို ဂရုတစိုက် နိုင်နိုင်နင်းနင်း သိတဲ့ သူဟာ သူကိုယ်တိုင်နဲ့ **တခြားသူ**တွေရော သူတို့ လိုချင်တဲ့ အတိုင်း အလုပ်လုပ်မယ်လို့ အသေအချာသိအောင် code တွေရေးမှာပါ။

bugs တွေအနည်းဆုံး သို့မဟုတ် မရှိတဲ့ နည်းစနစ်တွေ သုံးတဲ့ အခါ ယုံကြည်မှုလည်းမြင့်တက်လာပါတယ်။ အဲ့ဒါက FP ရဲ့ အကြီးဆုံး အားသာချက်လည်း ဖြစ်နိုင်ပါတယ်။ FP program တွေက bugs နည်းတယ်၊ ရှိရင်လည်း ထင်ရှားတဲ့ နေရာတွေမှာ ရှိတယ်၊ အဲ့ဒီ အတွက် ရှာပြီး ပြင်ဆင်ဖို့ လွယ်တယ်။ FP code တွေက bugs နည်းလေ့ ရှိပေမယ့် လုံးဝ မရှိဘူးပြောတာ မဟုတ်ပါဘူး။

ဒီစာအုပ်ဖတ်ရင်း  သင်ဟာ ယုံကြည်စိတ်ချရတဲ့ patterns တွေ practices တွေကို သုံးရင်း program bugs ဖြစ်လေ့ရှိတဲ့ အကြောင်းရင်းတွေ ရှောင်နိုင်မှာ ဖြစ်တဲ့ အတွက် သင်ရေးတဲ့ code ကို သင်ပိုယုံကြည်လာမှာပါ

## Communication

FP ဘာလို့ အရေးကြီးတာလဲ။ အဲ့ဒါကိုဖြေဖို့ ခပ်ဝေးဝေး နောက်ပြန်ဆုတ်ပြီး programming ကိုယ်တိုင်ကိုက ဘာလို့ အရေးကြီးတာလဲ ပြောဖို့လိုအပ်ပါတယ်။

သင်ဒါကိုကြားရင် အံ့သြမှာပါ။ ဒါပေမယ့် code ဆိုတာ computer အတွက် ညွှန်ကြားချက် အစုအဝေးလို့ ကျနော်တော့ မယုံပါဘူး။  တကယ်တော့ ကျနော်တော့ computer ကို code က ညွှန်ကြားတယ် ဆိုတာ မတော်တဆ ဖြစ်သွားတာပါ။

code ရဲ့ ပိုအရေးကြီးတဲ့ အပိုင်းက လူသားတွေ အချင်းချင်း ဆက်သွယ်ဖို့လို့ ကျနော် နက်နက်ရှိုင်းရှိုင်း ယုံကြည်ပါတယ်။

သင့်ရဲ့ coding အချိန်တော်တော်များများက ရှိပြီးသား code တွေဖတ်ရင်း ကုန်သွားတယ်ဆိုတာ အတွေ့အကြုံအရ သင်သိရင်သိမှာပါ။ လူအနည်းငယ်ပဲ အချိန်အများစုကို တခြားသူ(ကိုယ်ကိုယ်တိုင်) ရေးထားတဲ့ code တွေကြည့်စရာ မလိုပဲ code အသစ်တွေနဲ့ အချိန်ကုန်ခွင့်ရှိတာပါ။

 developer တွေရဲ့ အချိန် 70% ကို code ကို maintenance လုပ်ဖို့ ဖတ်ပြီး နားလည်ဖို့ ကြိုးစားရင်း ကုန်ဆုံးသွားတယ်လို့ တော်တော်များများ ခန့်မှန်းကြတယ်။ ဒါက မျက်စိပွင့်စေပါတယ်။ တကမ္ဘာလုံး အတိုင်းအတာနဲ့ ယှဉ်ရင် programmer တစ်ယောက်ရဲ့ တစ်နေ့ ရေးတဲ့ code အကြောင်းရေ 10 ကြောင်းလောက်ပဲရှိတာ အံသြစရာ မဟုတ်ပါဘူး။ ကျနော်တို့ဟာ ကျနော်တို့ရဲ့ တစ်နေ့တာကို အဲ့ဒီ code 10 ကြောင်း ဘယ်နားသွားရေးရမလဲ တွေးနေရတာနဲ့ အချိန်ကုန်တာပါ။


ကျနော်တော့ ကျနော်တို့ code တွေရဲ့ readability ကို ပို ဂရုစိုက်သင့်တယ် ထင်ပါတယ်။ ပြီးတော့ စကားမစပ် readability is not just about fewer characters. Readability is actually most impacted by familiarity. [1]

ကျနော်တို့ အချိန်တွေကို ဖတ်လွယ် နားလည်လွယ်အောင် ကြိုးစားမယ်ဆိုရင် FP က အဲ့ဒီ ကြိုးစားမှုမှာ အချက်အချာ ကျပါတယ်။ FP ရဲ့ စည်းကမ်းတွေဟာ အခြေကျပြီးသား၊ နက်နက်နဲနဲ လေ့လာပြီးသား ဖြစ်ပြီး သက်သေလည်းပြနိုင်ပါတယ်။ အဲ့ဒီ FP စည်းကမ်းတွေကို အချိန်ယူ သင်ပြီး အသုံးချခြင်းက သင်ကိုယ်တိုင် အတွက်ရော တခြားသူတွေ အတွက်ပါ လွယ်လွယ်ကူကူနဲ့ ရင်းနှီး မှတ်မိလွယ်တဲ့ code  တွေအဖြစ် ဉီးတည်စေမှာပါ။ code ရဲ့ ရင်းနှီးမှု နဲ့ မှတ်မိလွယ်မှု တိုးလာတာက code readability ပါ တိုးတက်စေပါတယ်။

ဉပမာ သင်က `map(..)` ဘယ်လိုအလုပ်လုပ်လဲ နားလည်ရင် တခြားဘယ် program မှာပဲ မြင်မြင် ချက်ခြင်းနားလည်နိုင်ပါတယ်။ ဒါပေမယ့် သင် `for`loop ကို မြင်တဲ့ အကြိမ်တိုင်းတော့ နားလည်ဖို့  loop တစ်ခုလုံး ဖတ်ရမှာပါ။ `for` loop ရဲ့ syntax ကို ရင်နှီးပေမယ့် ဘယ်လို အလုပ်လုပ်လဲကတော့ အမြဲတမ်း ဖတ်ကြည့်မှ သိရမှာပါ။

ကြည့်တာနဲ့ မှတ်မိတဲ့ code များများ ရှိခြင်းအားဖြင့် ဒီ code ဘယ်လို အလုပ်လုပ်လဲ တွေးရနဲပြီး ကျနော်တို့ရဲ့ အာရုံစိုက်မှုက ပိုအရေးကြီးတဲ့ program logic ကို တွေးနိုင်ပါတယ်။ အာရုံစိုက်ဖို့ အများဆုံးလိုအပ်တာကလည်း program logic ပါပဲ။

FP (အနည်းဆုံးတော့ အချက်အလက်တွေ အကုန်လုံး မနှိုင်းယှဉ်ဘဲ) readable code တွေ တည်ဆောက်ဖို့ အထိရောက်ဆုံး tools တွေထဲက တစ်ခုပါပဲ။ အဲ့ဒါကြောင့်ပဲ အရမ်းအရေးကြီးတာပါ။

## Readability

Readability က binary characteristic မဟုတ်ပါဘူး။ ကျနော်တို့တွေနဲ့ code တွေ ဘယ်လို ဆက်စပ်မှု ရှိလဲ ဆိုတာ လူသားတွေ ထည့်သွင်းစဉ်းစားတဲ့ အချက်အလက် ပေါ်မှာပဲ မူတည်ပါတယ်။ ကျနော်တို့ရဲ့ အရည်အချင်းတွေ နားလည်မှု ပေါ်မူတည်ပြီး ကျနော်တို့ရဲ့ အချိန်တွေက ကွဲပြားမှာပါ။
 
အောက်က ပုံလိုမျိုး သက်ရောက်မှုကို ကျနော်လည်း ခံစားဖူးတယ်။ ပြီးတော့ ကျနော်နဲ့ စကားပြောဖူးတဲ့ လူတော်တော်များများရောပဲ။


<p align="center">
    <img src="fig17.png" width="600">
</p>

ဒီစာအုပ်အတိုင်း လိုက်လုပ်ရင်း သင်လည်း ပုံစံတူ ခံစားရနိုင်ပေမယ့် မပူပါနဲ့ ဆက်သာလုပ်သွားပါ။ curve က ပြန်တက်လာမှာပါ။

*Imperative* ဆိုတာ ကျနော်တို့ ရေးလေ့ ရှိတဲ့ code တွေကို ပြောတာပါ။ computer ကို တိတိကျကျ ဘယ်လို အလုပ်လုပ်ရမလဲ ညွှန်ကြားဖို့ အာရုံစိုက်တာပါ။ Declarative code က FP စည်းမျဉ်အတိုင်း ရေးဖို့သင်မယ့် အမျိုးအစားပါ။ ဘယ်လို outcome မျိုး ဖြစ်ရမလဲ ဆိုတဲ့ အပေါ်ပိုအာရုံထားပါတယ်။

အခု chapter အစက code snippets နှစ်ခုကို ပြန် ဆန်းစစ်ရအောင်။

The first snippet is imperative, focused almost entirely on *how* to do the tasks; it's littered with `if` statements, `for` loops, temporary variables, reassignments, value mutations, function calls with side effects, and implicit data flow between functions. You certainly *can* trace through its logic to see how the numbers flow and change to the end state, but it's not at all clear and straightforward.


The second snippet is more declarative; it does away with most of those aforementioned imperative techniques. Notice there's no explicit conditionals, loops, side effects, reassignments, or mutations; instead, it employs well-known (to the FP world, anyway!) and trustable patterns like filtering, reduction, transducing, and composition. The focus shifts from low-level *how* to higher level *what* outcomes.

Instead of messing with an `if` statement to test a number, we delegate that to a well-known FP utility like `gte(..)` (greater-than-or-equal-to), and then focus on the more important task of combining that filter with another filter and a summation function.

Moreover, the flow of data through the second program is explicit:

1. A list of numbers goes into `printMagicNumber(..)`.
2. One at a time those numbers are processed by `sumOnlyFavorites(..)`, resulting in a single number total of only our favorite kinds of numbers.
3. That total is converted to a message string with `constructMsg(..)`.
4. The message string is printed to the console with `console.log(..)`.

You may still feel this approach is convoluted, and that the imperative snippet was easier to understand. You're much more used to it; familiarity has a profound influence on our judgements of readability. By the end of this book, though, you will have internalized the benefits of the second snippet's declarative approach, and that familiarity will spring its readability to life.

I know asking you to believe that at this point is a leap of faith.

It takes a lot more effort, and sometimes more code, to improve its readability as I'm suggesting, and to minimize or eliminate many of the mistakes that lead to bugs. Quite honestly, when I started writing this book, I could never have written (or even fully understood!) that second snippet. As I'm now further along on my journey of learning, it's more natural and comfortable.

If you're hoping that FP refactoring, like a magic silver bullet, will quickly transform your code to be more graceful, elegant, clever, resiliant, and concise -- that it will come easy in the short term -- unfortunately that's just not a realistic expectation.

FP is a very different way of thinking about how code should be structured, to make the flow of data much more obvious and to help your reader follow your thinking. It will take time. This effort is eminently worthwhile, but it can be an arduous journey.

It still often takes me multiple attempts at refactoring a snippet of imperative code into more declarative FP, before I end up with something that's clear enough for me to understand later. I've found converting to FP is a slow iterative process rather than a quick binary flip from one paradigm to another.

I also apply the "teach it later" test to every piece of code I write. After I've written a piece of code, I leave it alone for a few hours or days, then come back and try to read it with fresh eyes, and pretend as if I need to teach or explain it to someone else. Usually, it's jumbled and confusing the first few passes, so I tweak it and repeat!

I'm not trying to dampen your spirits. I really want you to hack through these weeds. I am glad I have. I can finally start to see the curve bending upward towards more readability. The effort has been worth it. It will be for you, too.

## Perspective

We're going to approach FP from the ground up -- it seems to me most other FP texts go the opposite direction: top-down -- and discover the basic foundational principles that I believe formal FPers would admit are the scaffolding for everything they do. But for the most part we'll stay arms length away from most of the intimidating terminology or mathematical notation that can so easily frustrate learners.

I believe it's less important what you call something and more important that you understand what it is and how it works. That's not to say there's no importance to shared terminology -- it undoubtedly eases communication among seasoned professionals. But for the learner, I've found it can be distracting.

So this book will try to focus more on the base concepts and less on the fancy fluff. That's not to say there won't be terminology; there definitely will be. But don't get too wrapped up in the sophisticated words. Wherever necessary, look beyond them to the ideas.

I call the less formal practice herein "Functional-Light Programming" because I think where the formalism of true FP suffers is that it can be quite overwhelming if you're not already accustomed to formal thought. I'm not just guessing; this is my own personal story. Even after teaching FP and writing this book, I can still say that the formalism of terms and notation in FP is very, very diffcult for me to process. I've tried, and tried, and I can't seem to get through much of it.

I know many FPers who believe that the formalism itself helps learning. But I think there's clearly a cliff where that only becomes true once you reach a certain comfort with the formalism. If you happen to already have a math background or even some flavors of CS experience, this may come more naturally to you. But some of us don't, and no matter how hard we try, the formalism keeps getting in the way.

So this book introduces the concepts that I believe FP is built on, but comes at it by giving you a boost from below to climb up the cliff wall, rather than condescendingly shouting down at you from the top, proding you to just figure out how to climb as you go.

## How To Find Balance

If you've been around programming for very long, chances are you've heard the phrase "YAGNI" before: "You Ain't Gonna Need It". This principle primarily comes from extreme programming, and stresses the high risk and cost of building a feature before it's needed.

Sometimes we guess we'll need a feature in the future, build it now believing it'll be easier to do as we build other stuff, then realize we guessed wrong and the feature wasn't needed, or needed to be quite different. Other times we guess right, but build a feature too early, and suck up time from the features that are genuinely needed now; we incur an opportunity cost in diluting our energy.

YAGNI challenges us to remember: even if it's counter intuitive in a situation, we often should postpone building something until it's presently needed. We tend to exaggerate our mental estimates of the future refactoring cost of adding it later when it is needed. Odds are, it won't be as hard to do later as we might assume.

As it applies to functional programming, I would offer this admonition: there will be plenty of interesting and compelling patterns discussed in this text, but just because you find some pattern exciting to apply, it may not necessarily be appropriate to do so in a given part of your code.

This is where I will differ from many formal FPers: just because you *can* apply FP to something doesn't mean you *should* apply FP to it. Moreover, there are many ways to slice a problem, and even though you may have learned a more sophisticated approach that is more "future-proof" to maintenance and extensibility, a simpler FP pattern might be more than sufficient in that spot.

Generally, I'd recommend to seek balance in what you code, and to be conservative in your application of FP concepts as you get the hang of things. Default to the YAGNI principle in deciding if a certain pattern or abstraction will help that part of the code be more readable or if it's just introducing clever sophistication that isn't (yet) warranted.

> Reminder, any extensibility point that’s never used isn’t just wasted effort, it’s likely to also get in your way as well
>
> Jeremy D. Miller @jeremydmiller 2/20/15
>
> https://twitter.com/jeremydmiller/status/568797862441586688

Remember, every single line of code you write has a reader cost associated with it. That reader may be another team member, or even your future self. Neither of those readers will be impressed with overly clever, unnecessary sophistication just to show off your FP prowess.

The best code is the code that is most readable in the future because it strikes exactly the right balance between what it can/should be (idealism) and what it must be (pragmatism).

## Resources

I have drawn on a great many different resources to be able to compose this text. I believe you, too, may benefit from them, so I wanted to take a moment to point them out.

### Books

Some FP/JavaScript books that you should definitely read:

* [Professor Frisby's Mostly Adequate Guide to Functional Programming](https://drboolean.gitbooks.io/mostly-adequate-guide/content/ch1.html) by [Brian Lonsdorf](https://twitter.com/drboolean)
* [JavaScript Allongé](https://leanpub.com/javascriptallongesix) by [Reg Braithwaite](https://twitter.com/raganwald)
* [Functional JavaScript](http://shop.oreilly.com/product/0636920028857.do) by [Michael Fogus](https://twitter.com/fogus)

### Blogs/Sites

Some other authors and content you should check out:

* [Fun Fun Function Videos](https://www.youtube.com/watch?v=BMUiFMZr7vk) by [Mattias P Johansson](https://twitter.com/mpjme)
* [Awesome FP JS](https://github.com/stoeffel/awesome-fp-js)
* [Kris Jenkins](http://blog.jenkster.com/2015/12/what-is-functional-programming.html)
* [Eric Elliott](https://medium.com/@_ericelliott)
* [James A Forbes](https://james-forbes.com/)
* [James Longster](https://github.com/jlongster)
* [André Staltz](http://staltz.com/)
* [Functional Programming Jargon](https://github.com/hemanth/functional-programming-jargon#functional-programming-jargon)
* [Functional Programming Exercises](https://github.com/InceptionCode/Functional-Programming-Exercises)

### Libraries

The code snippets in this book largely do not rely on libraries. Each operation that we discover, we'll derive how to implement it in standalone, plain ol' JavaScript. However, as you begin to build more of your real code with FP, you'll quickly want a library to provide optimized and highly reliable versions of these commonly accepted utilities.

By the way, you'll want to make sure you check the documentation for the library functions you use to make sure you know how they work. There will be a lot of similarities in many of them to the code we build on in this text, but there will undoubtedly be some differences, even between popular libraries.

Here are a few popular FP libraries for JavaScript that are a great place to start your exploration with:

* [Ramda](http://ramdajs.com)
* [lodash/fp](https://github.com/lodash/lodash/wiki/FP-Guide)
* [functional.js](http://functionaljs.com/)
* [Immutable.js](https://github.com/facebook/immutable-js)

Appendix C takes a deeper look at these libraries and others.

## Summary

You may have a variety reasons for starting to read this book, and different expectations of what you'll get out of it. This chapter has explained why I want you to read the book and what I want you to get out of the journey. It also helps you articulate to others (like your fellow developers) why they should come on the journey with you!

Functional programming is about writing code that is based on proven principles so we can gain a level of confidence and trust over the code we write and read. We shouldn't be content to write code that we anxiously *hope* works, and then abruptly breathe a sigh of relief when the test suite passes. We should *know* what it will do before we run it, and we should be absolutely confident that we've communicated all these ideas in our code for the benefit of other readers (including our future selves).

This is the heart of Functional-Light JavaScript. The goal is to learn to effectively communicate with our code but not have to suffocate under mountains of notation or terminology to get there.

The journey to learning functional programming starts with deeply understanding the nature of what a function is. That's what we tackle in the next chapter.

----

[1] Buse, Raymond P. L., and Westley R. Weimer. “Learning a Metric for Code Readability.” IEEE Transactions on Software Engineering, IEEE Press, July 2010, dl.acm.org/citation.cfm?id=1850615.
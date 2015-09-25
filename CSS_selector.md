# CSS selector

## Class 選擇器
```css
.class {}
```

## ID 選擇器
```css
#id {}
```

## 標籤選擇器
```css
tagname {}
```

## 通用選擇器
```css
* {}
``` 
WTF is this? Better not using it.

## 屬性選擇器
```css
element[attribute] {}
element[attribute="blabla"] {}
/* Regex selector  */
element[attribute*="val"] {} /* catch elements with attribute's value  which containing substring "val"  */
element[attribute^="val"] {} /* catch value starts with "val" */
element[attribute$="val"] {} /* catch value ends with "val" */
```

## 群組選擇器
```css
elementA, elementB, elementC {}
```

## 後代選擇器
```css
elementA elementB {} // 找出 elementA 以下所有的 elementB
elementA > elementB {} // 找出 elementA 僅下一層的 elementB
```

## 同層選擇器
```css
eleA + eleB {}
```
__同層相鄰__ 找出位置在同一層，且接在 eleA 之後的__第一個__ eleB。

```css
eleA ~ eleB {}
```
__同層全體__ 找出位置在同一層，且接在 eleA 之後的__所有__ eleB。

## 偽類選擇器：根據元素之狀態與條件選取元素
```css
element:link
element:visited
element:hover
element:focus
element:not(selector)
...
```

## 偽元素選擇器
```css
element:first-line
element:first-letter
element::after
element::before
```






















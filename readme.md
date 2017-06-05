# [WIP] PostCSS - Typography Parser utility

> PostCSS plugin that walk through you css declarations to find the dynamic font values and enforce a predefined one. This plugin is part of [Salt](https://github.com/alexandremasy/salt), a collection of tool to help you enforce a set of rule througout your application.



## Getting started

Installation is as easy as:

```shell
npm install postcss-salt-typography-parser
```



**PostCSS**

Include the plugin in you build process:

```
@TODO

```

**Gulp**

Include the plugin in your build process:

```
@TODO
```



This plugins depends on :

- [PostCSS](https://github.com/postcss/postcss)
- [Salt - Typography - Helper](https://github.com/alexandremasy/postcss-salt-typography-helper)
- [Salt - Layout - Breakpoint](https://github.com/alexandremasy/postcss-salt-layout-breakpoint)





## Functionalities

Walk through your typographic css declarations to find the dynamic values and enforce a predefined one;

 ```css
html
{
  #font-family: <domain>;
  #font-weight: <domain>? / <weights>;
  #font-size: <domain>? / <scale>;
  #line-height: <domain>? / <scale>;
  #font-style: <domain>? / [italic | oblique | none];
}
 ```



------



### #font-family

Define a font-family. 

```css
#font-family: <domain>;
```

| Property              | Type   | Description                              |
| --------------------- | ------ | ---------------------------------------- |
| `domain` **required** | String | the name defined in the [font definition option](https://github.com/alexandremasy/postcss-salt-typography#configuration). If the given value is not found in the definition, the plugin will throw an exception. |



**will yield**

```css
font-family: <family>
```

| Property | Type   | Description                              |
| -------- | ------ | ---------------------------------------- |
| `family` | String | The family value in the [font definition option](https://github.com/alexandremasy/postcss-salt-typography#configuration). |



------



### #font-weight

Define a font-weight

```css
#font-weight: <domain>? / <weight>;
```

| Property              | Type   | Description                              |
| --------------------- | ------ | ---------------------------------------- |
| `domain` *optional*   | String | the name defined in the [font definition option](https://github.com/alexandremasy/postcss-salt-typography#configuration). If not provided, we'll take the first entry in the font definition. If the given value is not found in the definition, the plugin will throw an exception. |
| `weight` **required** | String | One of the [allowed weight values](https://github.com/alexandremasy/postcss-salt-typography#weight). |



**will yield**

```css
font-weight: <weight>
```

| Property | Type   | Description                   |
| -------- | ------ | ----------------------------- |
| `weight` | Number | The weight of the given font. |



------



### #font-size

Define a font-size

```css
#font-size: <domain>? / <scale>;
```

| Property             | Type   | Description                              |
| -------------------- | ------ | ---------------------------------------- |
| `domain` *optional*  | String | the name defined in the [font definition option](https://github.com/alexandremasy/postcss-salt-typography#configuration). If not provided, we'll take the first entry in the font definition. If the given value is not found in the definition, the plugin will throw an exception. |
| `scale` **required** | String | One of the scale you defined in your font definition option. |



**will yield for a singular scale value**

```css
font-size: <length>
```

| Property | Type   | Description               |
| -------- | ------ | ------------------------- |
| `length` | Number | The defined length value. |



**will yield for a dual scale value**

```css
font-size: calc((<font-first> * <unit>) + (<font-last> - <font-first>) * (100vw - <breakpoint-first>) / (<breakpoint-last> - <breakpoint-first>));

@breakpoint('><breakpoint-last>')
{
  font-size: <font-last> * <unit>;
}

@breakpoint('<<breakpoint-first>')
{
  font-size: <font-first> * <unit>;
}
```

| Property           | Type   | Description                              |
| ------------------ | ------ | ---------------------------------------- |
| `font-first`       | Number | The first value in the scale declaration. |
| `font-last`        | Number | The last value in the scale declaration. |
| `unit`             | Number | The unit used for the font-size, computed from the scale declaration. |
| `breakpoint-first` | Number | The first value in the breakpoint declaration. |
| `breakpoint-last`  | Number | The last value in the breakpoint declaration. |



------



### #line-height

Define a line-height

```css
#line-height: <domain>? / <scale>;
```

| Property             | Type   | Description                              |
| -------------------- | ------ | ---------------------------------------- |
| `domain` *optional*  | String | the name defined in the [font definition option](https://github.com/alexandremasy/postcss-salt-typography#configuration). If not provided, we'll take the first entry in the font definition. If the given value is not found in the definition, the plugin will throw an exception. |
| `scale` **required** | String | One of the scale you defined in your font definition option. |



**will yield for a singular scale value**

```css
line-height: <length>
```

| Property | Type   | Description               |
| -------- | ------ | ------------------------- |
| `length` | Number | The defined length value. |



**will yield for a dual scale value**

```css
line-height: calc((<height-first> * <unit>) + (<height-last> - <height-first>) * (100vw - <breakpoint-first>) / (<breakpoint-last> - <breakpoint-first>));

@breakpoint('><breakpoint-last>')
{
  font-size: <height-last> * <unit>;
}

@breakpoint('<<breakpoint-first>')
{
  font-size: <height-last> * <unit>;
}
```

| Property           | Type   | Description                              |
| ------------------ | ------ | ---------------------------------------- |
| `height-first`     | Number | The first value in the scale declaration. |
| `height-last`      | Number | The last value in the scale declaration. |
| `unit`             | Number | The unit used for the font-size, computed from the scale declaration. |
| `breakpoint-first` | Number | The first value in the breakpoint declaration. |
| `breakpoint-last`  | Number | The last value in the breakpoint declaration. |



------



### #font-style

Define a font-style

```css
#font-size: <domain>? / [italic | oblique | none];
```

| Property                                 | Type   | Description                              |
| ---------------------------------------- | ------ | ---------------------------------------- |
| `domain` *optional*                      | String | the name defined in the [font definition option](https://github.com/alexandremasy/postcss-salt-typography#configuration). If the given value is not found in the definition, the plugin will throw an exception. If not provided, we'll take the first entry in the font definition with the given style. It no entry is found, an exception will be thrown. |
| `italic` `oblique` `normal` **required** | String | One of these value.                      |



**will yield**

```css
font-style: [italic | oblique | normal]
```

| Property | Type   | Description               |
| -------- | ------ | ------------------------- |
| `length` | Number | The defined length value. |


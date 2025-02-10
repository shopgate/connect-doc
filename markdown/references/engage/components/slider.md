---
stoplight-id: uvt9fotcs27g3
---

# Slider/Swiper
The `Slider` component is a mobile touch slider with hardware accelerated transitions.

## Why use it
The `Slider` component builds the slider so that the developer does not have to build their own slider.
It uses the [iDangerous Swiper](https://idangero.us/swiper/) under the hood.


## Props

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| __children__* | node | | The swiper content
| autoPlay | boolean | `false` | Whether to enable autoplay
| interval | number | `3000` | Delay between transitions (in ms)
| controls | object \| boolean | `false` | Whether to show controls for prev and next slide. Check [IDSwiper API](https://idangero.us/swiper/api/#navigation) for the object use.
| className | string | `null` | Class name for styling
| classNames | object | `{}`| Class names for specific elements. Available elements `container`, `item`, `bulletClass`, `bulletActiveClass`<br><br>Example:<br>`{bulletActiveClass: 'active-bullet'}`
| rebuildOnUpdate | boolean | `true` | Whether to rebuild swiper when component is updated
| initialSlide | number | `0` | Index number of initial slide
| slidesPerView | number | `1` | Number of slides per view (slides visible at the same time on slider's container). Is always `1` if `loop` is set to`true`.
| indicators | boolean | `false` | Whether to show pagination (e.g. bullets)
| loop | boolean | `false` | Whether to enable continuous loop mode
| freeMode | boolean | `false` | Whether slides have fixed positions. If `true` then slides do not have fixed positions.
| onSlideChange | function | | Callback invoked when currently active slide is changed
| zoom | object &#124; boolean | `false` | Enables zoom functionality. Object with zoom parameters or boolean `true` to enable with default settings.
| disabled | boolean | `false` | Whether to disable swiping to previous or next slide
| * |  |  | Additionally, you can use every [param](https://idangero.us/swiper/api/#parameters) from the IDSwiper and it simply passes through.

## Slider.Item
A wrapper for a single slide of the slider.

### Props

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| __children__* | node | | The item content |
| className | string | `null` | className for styling


## Usage

```jsx
import { Slider } from '@shopgate/engage/components';

const slides = [
    {
      id: 1,
      content: 'My first slide',
    },
    {
      id: 2,
      content: 'My second slide',
    }
];

const Component = () => (
    <Slider
        loop={true}
        autoPlay={true}
    >
        {slides.map((slide) => (
            <Slider.Item key={slide.id)}>
              <p>{slide.content}</p>
            </Slider.Item>
        ))}
    </Slider>
);

export default Component;
```
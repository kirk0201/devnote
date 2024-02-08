[toc]

# Swiper Button 커스터마이징

---

- nextjs는 global.css에 작성해주면 작동함

```css
// Swiper 화살표 숨김
.swiper-button-next::after,
.swiper-button-prev::after {
    display: none;
}

// Swiper 화살표 이미지 변경
.swiper-button-prev {
    background: url(변경할 화살표 이미지) no-repeat;
}
.swiper-button-next {
    background: url(변경할 화살표 이미지) no-repeat;
}

// 투명도 및 크기 조절
.swiper-button-prev,
.swiper-button-next {
    opacity: 0.7;
    background-size: 70% auto;
    background-position: center;
}
```


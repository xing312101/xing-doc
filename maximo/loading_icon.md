# loading icon

## Html
```
<div style="display: block; cursor: wait; opacity: 1;">
    <div class="bx--loading-overlay">
      <div data-loading="" class="bx--loading">
        <svg class="bx--loading__svg" viewBox="-75 -75 150 150">
          <title>Loading</title>
          <circle cx="0" cy="0" r="37.5"></circle>
        </svg>
      </div>
    </div>
  </div>
```

## CSS
```
@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes rotate-end-p1 {
  100% {
    transform: rotate(360deg);
  }
}

@keyframes rotate-end-p2 {
  100% {
    transform: rotate(-360deg);
  }
}

@keyframes init-stroke {
  0% {
    stroke-dashoffset: 240;
  }
  100% {
    stroke-dashoffset: 40;
  }
}

@keyframes stroke-end {
  0% {
    stroke-dashoffset: 40;
  }
  100% {
    stroke-dashoffset: 240;
  }
}
.bx--loading {
  animation-name: rotate;
  animation-duration: 500ms;
  animation-timing-function: linear;
  animation-fill-mode: forwards;
  animation-iteration-count: infinite;

  width: 10.5rem;
  height: 10.5rem;
}

.bx--loading svg circle {
  animation-name: init-stroke;
  animation-duration: 1000ms;
  animation-timing-function: cubic-bezier(0.5, 0, 0.1, 1);
}

.bx--loading__svg {
  fill: transparent;
  stroke: #5aaafa;
  stroke-width: 7;
  stroke-linecap: butt;
  stroke-dasharray: 240;
  stroke-dashoffset: 40;
}

.bx--loading--stop {
  animation: rotate-end-p1 700ms cubic-bezier(0, 0, 0.25, 1) forwards, rotate-end-p2 700ms cubic-bezier(0, 0, 0.25, 1) 700ms forwards;
}

.bx--loading--stop svg circle {
  animation-name: stroke-end;
  animation-duration: 700ms;
  animation-timing-function: cubic-bezier(0, 0, 0.25, 1);
  animation-delay: 700ms;
  animation-fill-mode: forwards;
}

.bx--loading--small {
  width: 2rem;
  height: 2rem;
}

.bx--loading--small .bx--loading__svg {
  stroke: #8c9ba5;
}

.bx--loading-overlay {
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background-color: rgba(255, 255, 255, 0.6);
  display: -ms-flexbox;
  display: flex;
  -ms-flex-pack: center;
  justify-content: center;
  -ms-flex-align: center;
  align-items: center;
  transition: background-color 2000ms cubic-bezier(0.5, 0, 0.1, 1);
  z-index: 8000;
}

.bx--loading-overlay--stop {
  display: none;
}
```


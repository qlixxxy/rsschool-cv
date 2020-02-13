# Resume for RSS
1. Anton Sargan.
2. Mobile phone *+375 (29) 257-82-37*; VK - *[VK](https://vk.com/qlixor)*
3. I want to learn professional website layout. I always dreamed of creating something myself, creating something that ordinary people would use. It has always been interesting how the structure of what has become an integral part of our lives is arranged - a worldwide network. Having studied the theory myself, I plunged headlong into the world of front-end. Someday I want to get into a team where they create some useful non-profit sites. A few words to myself: I am 22 years old, my current place of work is one of the Big Four audit firms. There I developed a skill of resistance to stress to a state close to perfect. But the very kind of audit activity does not quite fit into my ideals due to the almost complete lack of creativity. Despite this, I quickly got promoted at my previous job and am already partially leading some small projects. A few more facts: I love sports, all sorts of different activities, where you need to do something / unravel / solve with the forces of the whole team.
4. Since I worked in an audit firm, we had to work with Client information through Excel tools. Most often, the information there is unprocessed, and the project team has to devote a lot of time to the primary processing of information: breaking down text, formatting numbers, dates, breaking down into columns and rows, improving readability, etc. Sometimes standard tools are not enough and we write macros through VBA. So I have some knowledge in this area. He graduated from RSS courses, having studied in detail the layout of the site using Flexbox and Grid. And also fully mastered CoreJS.
5. Code example:
```javascript
    import {
    setCurrentColor
} from '../tool/color.js';
import {
    setCurrentTool,
    setPixelSize,
    renderPixelSize
} from '../tool/tools.js';
import {
    storedActiveFrame,
    addFrame,
    deleteFrame,
    copyFrame,
    renderFrames,
    setActiveFrame
} from '../frames/frame.js';
import {
    drawMatrix,
    storedMatrixList,
    mainCanvas
} from '../canvas/canvas.js';
import {
    fullScreen
} from '../animation/animation.js';
import {
    saveAsGIF
} from '../animation/saveAnimationAsGIF.js';
import {
    saveAsAPNG
} from '../animation/saveAnimationAsAPNG.js';
import {
    openCloseModalWindow
} from '../modalWindow/modalWindow.js'

if (localStorage.activeTool === undefined) {
    localStorage.activeTool = 'pencil';
}

const colorCurrent = document.querySelector('#current');
const colorPrev = document.querySelector('#prev');
const colorCurrentLabel = document.querySelector("label[for=current]");
const colorPrevLabel = document.querySelector("label[for=prev]");
const INCREMENT = 1;
const DECREMENT = -1;

export let activeTool = localStorage.activeTool;

export let keyboardShortcuts = {
    bucket: 'KeyB',
    bucketAll: 'KeyA',
    eyedropper: 'KeyC',
    pencil: 'KeyP',
    eraser: 'KeyE',
    swapColors: 'KeyX',
    pixelSizeIncrement: 'BracketRight',
    pixelSizeDecrement: 'BracketLeft',
    addNewFrame: 'KeyN',
    deleteFrame: 'Delete',
    duplicateFrame: 'KeyD',
    nextFrame: 'ArrowDown',
    prevFrame: 'ArrowUp',
    saveGif: 'KeyG',
    saveApng: 'KeyS',
    fullScreen: 'KeyF',
    keyboardShortcutsWindow: 'KeyH'
}

document.addEventListener('keydown', function (event) {
    switch (event.code) {
        case keyboardShortcuts.bucket:
            activeTool = 'bucket';
            setCurrentTool();
            break;
        case keyboardShortcuts.eyedropper:
            activeTool = 'eyedropper';
            setCurrentTool();
            break;
        case keyboardShortcuts.pencil:
            activeTool = 'pencil';
            setCurrentTool();
            break;
        case keyboardShortcuts.bucketAll:
            activeTool = 'bucket_all';
            setCurrentTool();
            break;
        case keyboardShortcuts.eraser:
            activeTool = 'eraser';
            setCurrentTool();
            break;
        case keyboardShortcuts.addNewFrame:
            addFrame();
            break;
        case keyboardShortcuts.deleteFrame:
            deleteFrame(storedActiveFrame);
            break;
        case keyboardShortcuts.duplicateFrame:
            copyFrame(storedActiveFrame);
            break;
        case keyboardShortcuts.swapColors:
            setCurrentColor(colorPrev.value);
            break;
        case keyboardShortcuts.keyboardShortcutsWindow:
            openCloseModalWindow();
            break;
        case keyboardShortcuts.nextFrame:
            setActiveFrame(INCREMENT);
            break;
        case keyboardShortcuts.prevFrame:
            setActiveFrame(DECREMENT);
            break;
        case keyboardShortcuts.pixelSizeIncrement:
            setPixelSize(INCREMENT);
            renderPixelSize();
            break;
        case keyboardShortcuts.pixelSizeDecrement:
            setPixelSize(DECREMENT);
            renderPixelSize();
            break;
        case keyboardShortcuts.saveGif:
            saveAsGIF();
            break;
        case keyboardShortcuts.saveApng:
            saveAsAPNG();
            break;
        case keyboardShortcuts.fullScreen:
            fullScreen();
            break;
        default:
            break;
    }
    renderFrames();
    drawMatrix(mainCanvas, storedMatrixList[storedActiveFrame]);
});

document.querySelector('.bucket').addEventListener('click', function (event) {
    activeTool = 'bucket';
    setCurrentTool();
});

document.querySelector('.bucket_all').addEventListener('click', function (event) {
    activeTool = 'bucket_all';
    setCurrentTool();
});

document.querySelector('.eyedropper').addEventListener('click', function (event) {
    activeTool = 'eyedropper';
    setCurrentTool();
});

document.querySelector('.pencil').addEventListener('click', function (event) {
    activeTool = 'pencil';
    setCurrentTool();
});

document.querySelector('.eraser').addEventListener('click', function (event) {
    activeTool = 'eraser';
    setCurrentTool();
});

colorCurrent.addEventListener("change", function () {
    colorPrevLabel.style.background = colorCurrentLabel.style.background;
    colorCurrentLabel.style.background = colorCurrent.value;
    colorPrev.value = localStorage.currentColor;
    colorPrevLabel.style.background = colorPrev.value;
    localStorage.currentColor = colorCurrent.value;
    localStorage.prevColor = colorPrev.value;
});

colorPrev.addEventListener("change", function () {
    colorPrevLabel.style.background = colorPrev.value;
});

document.querySelector('.swap_color').addEventListener('click', function (event) {
    setCurrentColor(colorPrev.value);
});

document.querySelector('.prev_color').addEventListener('click', function (event) {
    setCurrentColor(colorPrev.value);
});
```
6. Expirience:  Macros written using VBA at previous job (for 2 years).
7. Education: BSU Faculty of Economics (2015-2019). RSS courses in 2020.
8. English level: Upper-intermediate. at the previous work, there were a lot of projects in English, since the clients were from abroad. I traveled to America for 2 months under the YLP student exchange program. There was also an advanced English course at the university.

# Resume for RSS
1. Anton Sargan.
2. Mobile phone *+375 (29) 257-82-37*; VK - *[VK](https://vk.com/qlixor)*
3. I want to learn professional website layout. I always dreamed of creating something myself, creating something that ordinary people would use. It has always been interesting how the structure of what has become an integral part of our lives is arranged - a worldwide network. Having studied the theory myself, I plunged headlong into the world of front-end. Someday I want to get into a team where they create some useful non-profit sites. A few words to myself: I am 22 years old, my current place of work is one of the Big Four audit firms. There I developed a skill of resistance to stress to a state close to perfect. But the very kind of audit activity does not quite fit into my ideals due to the almost complete lack of creativity. Despite this, I quickly got promoted at my previous job and am already partially leading some small projects. A few more facts: I love sports, all sorts of different activities, where you need to do something / unravel / solve with the forces of the whole team.
4. Since I worked in an audit firm, we had to work with Client information through Excel tools. Most often, the information there is unprocessed, and the project team has to devote a lot of time to the primary processing of information: breaking down text, formatting numbers, dates, breaking down into columns and rows, improving readability, etc. Sometimes standard tools are not enough and we write macros through VBA. So I have some knowledge in this area. He graduated from RSS courses, having studied in detail the layout of the site using Flexbox and Grid. And also fully mastered CoreJS.
5. Code example:
    ```javascript
    import {
    drawMatrix,
    storedMatrixList,
    addClearMatrix,
    mainCanvas
    } from '../canvas/canvas.js';

    import {
    zeroingStepFrame
    } from '../animation/animation.js';

    import {keyboardShortcuts} from '../action/action.js';

    import {setTooltip} from '../action/tooltip.js'

    const frameListArea = document.querySelector('.frame__list_area');
    const addFrameButton = document.createElement('div');
    const addFrameIcon = document.createElement('i');
    const addFrameLabel = document.createElement('div');
    const CANVAS_SIZE = 512;
    export const framesList = [];


    if (localStorage.activeFrame === undefined) {
    localStorage.activeFrame = 0;
    }

    if (localStorage.countFrames === undefined) {
    localStorage.countFrames = 1;
       }

    export let storedCountFrame = Number(localStorage.countFrames);
    export let storedActiveFrame = Number(localStorage.activeFrame);
 
    function createElementForFrame(tagName, className) {
    let element = document.createElement(tagName);
    element.className = className;
    return element;
    }
      
    export function addFrameElem() {
    let frameWrapper = createElementForFrame('li', 'frame_wrapper');
    let frameIndex = createElementForFrame('div', 'frame_index frame_button');
    let frameDeleteButton = createElementForFrame('div', 'frame_delete_button frame_button');
    let frameDeleteButtonIcon = createElementForFrame('i', 'fas fa-trash-alt');
    frameDeleteButton.append(frameDeleteButtonIcon);
    setTooltip(frameDeleteButton, 'Delete frame', keyboardShortcuts.deleteFrame);
    let frameCopyButton = createElementForFrame('div', 'frame_copy_button frame_button');
    let frameCopyButtonIcon = createElementForFrame('i', 'fas fa-copy');
    frameCopyButton.append(frameCopyButtonIcon);
    setTooltip(frameCopyButton, 'Duplicate frame', keyboardShortcuts.duplicateFrame);
    let canvas = createElementForFrame('canvas', 'frame_canvas');
    const ctx = canvas.getContext('2d');
    ctx.imageSmoothingEnabled = false;
    canvas.height = CANVAS_SIZE;
    canvas.width = CANVAS_SIZE;
    framesList.push({
        element: frameWrapper,
        canvasElem: canvas,
        indexElem: frameIndex,
        deleteButtonElem: frameDeleteButton,
        copyButtonElem: frameCopyButton
        });
        }

    export function deleteFrame(indexFrame) {
    if (storedCountFrame !== 1) {
        storedCountFrame -= 1;
        framesList.forEach((frame, index) => {
            if (index === indexFrame) {
                frame.element.remove();
            }
        })
        framesList.splice(indexFrame, 1);
        storedMatrixList.splice(indexFrame, 1);
        if (storedActiveFrame !== 0 && (indexFrame === storedActiveFrame || indexFrame < storedActiveFrame)) {
            storedActiveFrame -= 1;
        }
        zeroingStepFrame();
    }
   }

    export function copyFrame(indexFrame) {
    storedCountFrame += 1;
    storedActiveFrame = indexFrame + 1;
    addFrameElem();
    let copiedMatrix = storedMatrixList[indexFrame].slice();
    let matrix = copyMatrix(copiedMatrix);
    storedMatrixList.splice(indexFrame, 0, matrix);
   }

    function copyMatrix(copiedMatrix) {
    let size = copiedMatrix.length;
    return new Array(size).fill().map((value, index) => {
        const arr = new Array(size).fill().map((val, i) => {
            return copiedMatrix[index][i].slice();
        });
        return arr;
    });
    }

    function renderAddFrameButton() {
    addFrameButton.className = 'add__frame_button';
    addFrameIcon.className = 'fas fa-plus fa-fw';
    addFrameLabel.className = 'label';
    addFrameLabel.innerText = 'Add new frame';
    frameListArea.append(addFrameButton);
    addFrameButton.append(addFrameIcon);
    addFrameButton.append(addFrameLabel);
    setTooltip(addFrameButton, 'Add new frame', keyboardShortcuts.addNewFrame);
    }

    export function renderFrames() {
    console.log(storedMatrixList);
    framesList.forEach((frame, index) => {
        frameListArea.append(frame.element);
        frame.indexElem.innerText = index + 1;
        frame.element.append(frame.indexElem);
        frame.element.append(frame.canvasElem);
        frame.element.append(frame.deleteButtonElem);
        frame.element.append(frame.copyButtonElem);
        frame.element.classList.remove('active__frame_wrapper');
        if (framesList.length === 1) {
            frame.deleteButtonElem.style.display = 'none';
        } else {
            frame.deleteButtonElem.style.display = 'flex';
        }
        if (storedActiveFrame === index) {
            frame.element.classList.add('active__frame_wrapper');
        }
        drawMatrix(frame.canvasElem, storedMatrixList[index]);
    });
    renderAddFrameButton();
    }

    export function setActiveFrame(increment) {
    let possibleFrame = storedActiveFrame + increment;

    if (possibleFrame < storedCountFrame && possibleFrame >= 0) {
        storedActiveFrame = possibleFrame;
    }
    }

    export function addFrame() {
    storedCountFrame += 1;
    storedActiveFrame = storedCountFrame - 1;
    storedMatrixList.push(addClearMatrix(storedMatrixList[0].length));
    addFrameElem();
   }

   addFrameButton.addEventListener('click', addFrame);

    frameListArea.addEventListener('click', (event) => {
    let element = event.target;
    if (element.className === 'frame_canvas') {
        storedActiveFrame = element.parentNode.querySelector('.frame_index').innerText - 1;
    }
    if (element.tagName === 'I') {
        element = element.parentNode;
    }
    if (element.className.includes('frame_delete_button')) {
        let deletedFrameIndex = element.parentNode.querySelector('.frame_index').innerText - 1;
        deleteFrame(deletedFrameIndex);
    }
    if (element.className.includes('frame_copy_button')) {
        let copiedFrameIndex = element.parentNode.querySelector('.frame_index').innerText - 1;
        copyFrame(copiedFrameIndex);
    }
    renderFrames();
    drawMatrix(mainCanvas, storedMatrixList[storedActiveFrame]);
   })
```
6. Expirience:  Macros written using VBA at previous job (for 2 years).
7. Education: BSU Faculty of Economics (2015-2019). RSS courses in 2020.
8. English level: Upper-intermediate. at the previous work, there were a lot of projects in English, since the clients were from abroad. I traveled to America for 2 months under the YLP student exchange program. There was also an advanced English course at the university.

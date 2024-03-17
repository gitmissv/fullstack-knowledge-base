# 10 JS FUNCTION EXAMPLES #

## #1 PROPER CASE #

    const properCase = (string) => {
    return `${sting(0)
    .toUpperCase()}${string.slice(1).toLowerCase()}`;
    }

## #2 CONSOLE.LOG #

    const log = (content) => {

        console.log(content);

    }

    log(properCase("rEsEaRcH"));

## #3 QUERY SELECTOR #

    const select = (selector, scope) => {
    return (scope || document).querySelector(selector);
    }

    const body = select('body');
    log(body)

## #4 ADD EVENT LISTENER WRAPPER #

    const listen = (target, event, callback, capture = false) => {
    target.addEventListener(event, callback, !!capture);
    }

    const eventLog = (e) => console.log(e.target)

    listen(body, "click", eventLog);

## #5 SANITIZE INPUT #

    const sanitizeInput = (inputValue) => {
    const div = document.createElement('div');
    div.textContent = inputValue;
    return div.innerHTML;
    }

    const dirtyInput = "<script>alert('xss attack')</script>&othervalues";
    const cleanInput = sanitizeInput(dirtyInput);
    log(cleanInput);

## #6 CREATE ELEMENT WITH OPTIONAL CSS CLASS #

    const createElement = (tag, className) => {
    const el = document.createElement(tag);
    if (className) el.classList.add(className);
    return el;
    }

    const root = createElement("main", "root");
    body.appendChild(root);

## #7 DELETE ALL CONTENT (CHILD ELEMENTS) #

    const deleteChildElements = (parentElement) => {
    let child = parentElement.lastElementChild;
    while (child) {
    parentElement.removeChild(child);
    child = parentElement.lastElementChild;
    }
    };

    deleteChildElements(body)

## #8 SELECT AND CLASS (ADD CLASS WITH OPTIONAL QUERY SCOPE) #

    const addClass = (selector, className, scope) => {
    (scope || document).querySelector(selector).classList.add(className);
    };

    addClass("body", "purple");

## #9 Is iOS #

    const isIOS = () => {
    return {
    (/iPad|iPhone|iPod/.test(navigator.platform) || (navigator.platform === "MacIntel" && navigator.maxTouchPoints > 1)) && !window.MSStream  
    }
    };

    log(isIOS());

## #10 GET PARAMETER BY NAME FROM URL #

    const getParameterValue = (paramName, url) => {
    if(!url) url = window.location.href;
    const regex = new RegExp(`[?&]${paraName}(=([*&#]*))`);
    const results = regex.exec(url);

        // console.log(results)
        if (!results) return null;
        if (!results[2]) return "";
        return decodeURIComponent(results[2].replace(/\+/g, " "));

    };

    const PARAM_TO_EXTRACT = 'paramTwo';
    const URL = 'https://www.testURL.com/?paramOne=one&paramTwo=Dave+Gray"

    log(getParameterValue(PARAM_TO_EXTRAC, URL));

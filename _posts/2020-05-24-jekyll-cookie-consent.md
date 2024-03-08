---
categories: ['Webentwicklung']
tags: ['Jekyll', 'Static File CMS', 'Cookie']
title: 'Jekyll Cookie Consent Implementieren'
---

Auf ziemlich vielen Webseiten im Netz kommt Google Analytics zum Einsatz. Häufig werden die Cookies aber einfach gesetzt, ohne Zustimmung der User. Damit würdest Du dich datenschutzrechtlich auf dünnes Eis begeben. Damit Google Analytics (oder auch eine andere Tracking-Lösungen) DSGVO-konform einsetzbar ist, benötigst Du eine aktive Einwilligung / Erlaubnis deines Webseitenbesuchers. Auch wenn es nach wie vor sehr viele negative Beispiele für das willkürliche Setzen von Cookies gibt, möchtest Du es sicher gleich richtig machen. So verringerst Du nicht nur die Gefahr einer Abmahnung, sondern Du schützt auch ein Stück weit deine Webseitennutzer. Denn Du nutzt ja auch nicht ohne Grund Jekyll statt WordPress & Co.

### Osano hat die Lösung

Eine funktionierende Cookie Consent-Lösung bietet  [Osano](https://www.osano.com/cookieconsent){:target="_blank" rel="nofollow"}. Da das Projekt Open Source ist, liegt zum Glück so einiges an Code im  [Public-Repo von Osano](https://github.com/osano/cookieconsent){:target="_blank" rel="nofollow"}. Die benötigten Files mit Verlinkung folgen im weiteren Verlauf.

### Implementierung

**Anmerkung:**  Es gibt sicherlich viele Wege die letztendlich zum Ziel führen. Ich zeige Dir, wie ich es bei mir (testweise) DSGVO-konform und funktionstüchtig implementiert hatte._

Im ersten Schritt benötigst Du eine neue HTML-Datei unter `_includes` bzw. in ggf. Unterordner – entsprechend deiner Struktur. Nennen wir sie z.B. `cookieConsent.html`.

``` html
<link rel="stylesheet" type="text/css" href="{{ 'assets/css/cookieconsent.css' | absolute_url  }}" />
<script src="{{ 'assets/js/cookieconsent.min.js' | absolute_url  }}"></script>
<script>
    function loadGAonConsent() {
        window.ga = window.ga || function () {
            (ga.q = ga.q || []).push(arguments)
        };
        ga.l = +new Date;
        ga('create', 'UA-000000000-0', 'auto');
        ga('set', 'anonymizeIp', true);
        ga('send', 'pageview');
        var gascript = document.createElement("script");
        gascript.async = true;
        gascript.src = "https://www.google-analytics.com/analytics.js";
        document.getElementsByTagName("head")[0].appendChild(gascript, document.getElementsByTagName("head")[0]);
    }

    if (document.cookie.split(';').filter(function (item) {
            return item.indexOf('cookieconsent_status=allow') >= 0
        }).length) {
        loadGAonConsent();
    }

    window.addEventListener("load", function () {
        window.cookieconsent.initialise({
            "palette": {
                "popup": {
                    "background": "#313451"
                },
                "button": {
                    "background": "#4a4f79"
                }
            },
            "theme": "classic",
            "type": "opt-in",
            "content": {
                "message": "Ich nutze Cookies und Google Analytics, um diese Website für Dich so interessant wie möglich zu gestalten. Bist Du damit einverstanden? (Du kannst diese Entscheidung jederzeit widerrufen)",
                "deny": "Ablehnen",
                "allow": "OK, gerne!",
                "link": "Datenschutzhinweise",
                "href": "www.deineDomain.com/datenschutz.html"
            },
            onStatusChange: function (status, chosenBefore) {
                var type = this.options.type;
                var didConsent = this.hasConsented();
                if (type == 'opt-in' && didConsent) {
                    // enable cookies
                    loadGAonConsent();
                }
            }
        })
    });
</script>
```

_**Hinweis**: Bitte deine persönlichen Daten wie UA-Nr. und Link zur Datenschutzerklärung vor Verwendung anpassen._

Dieses File muss natürlich nun in dein Layout eingebunden werden. Hier eignet sich die Stelle hinter dem schließenden Footer-Tag (sofern vorhanden), wo auch deine anderen JS-Scripte aufgerufen werden.

```html
{% raw %}
</footer>
<!-- Scripts -->
{% include cookieConsent.html %}
<script src="{{ 'assets/js/blabla.min.js' | absolute_url  }}"></script>
{% endraw %}
```

Wie Du aber auch direkt am Anfang siehst, benötigen wir zwei weitere Dateien damit CookieConsent funktioniert. Nämlich eine `cookieconsent.css` und eine `cookieconsent.min.js`.

Das CSS-File könntest Du dir vom schon genannten  [Github-Repository](https://github.com/osano/cookieconsent){:target="_blank" rel="nofollow"}

```html
.cc-window {
    opacity: 1;
    transition: opacity 1s ease;
    margin:40px;
}

.cc-window.cc-invisible {
    opacity: 0
}

.cc-animate.cc-revoke {
    transition: transform 1s ease
}

.cc-animate.cc-revoke.cc-top {
    transform: translateY(-2em)
}

.cc-animate.cc-revoke.cc-bottom {
    transform: translateY(2em)
}

.cc-animate.cc-revoke.cc-active.cc-bottom,
.cc-animate.cc-revoke.cc-active.cc-top,
.cc-revoke:hover {
    transform: translateY(0)
}

.cc-grower {
    max-height: 0;
    overflow: hidden;
    transition: max-height 1s
}

.cc-link,
.cc-revoke:hover {
    text-decoration: none
}

.cc-revoke,
.cc-window {
    position: fixed;
    overflow: hidden;
    box-sizing: border-box;
    font-family: "Open Sans", sans-serif;
    font-size: 16px;
    line-height: 1.5em;
    display: -ms-flexbox;
    display: flex;
    -ms-flex-wrap: nowrap;
    flex-wrap: nowrap;
    z-index: 9999
}

.cc-window.cc-static {
    position: static
}

.cc-window.cc-floating {
    padding: 2em;
    max-width: 17em;
    -ms-flex-direction: column;
    flex-direction: column
}

.cc-window.cc-banner {
    padding: 1em 1.8em;
    width: 100%;
    -ms-flex-direction: row;
    flex-direction: row
}

.cc-revoke {
    padding: .5em
}

.cc-header {
    font-size: 18px;
    font-weight: 700
}

.cc-btn,
.cc-close,
.cc-link,
.cc-revoke {
    cursor: pointer
}

.cc-link {
    opacity: .8;
    display: inline-block;
    padding: .2em
}

.cc-link:hover {
    opacity: 1
}

.cc-link:active,
.cc-link:visited {
    color: initial
}

.cc-btn {
    display: block;
    padding: .4em .8em;
    font-size: .9em;
    font-weight: 700;
    border-width: 2px;
    border-style: solid;
    text-align: center;
    white-space: nowrap
}

.cc-highlight .cc-btn:first-child {
    background-color: transparent;
    border-color: transparent
}

.cc-highlight .cc-btn:first-child:focus,
.cc-highlight .cc-btn:first-child:hover {
    background-color: transparent;
    text-decoration: underline
}

.cc-close {
    display: block;
    position: absolute;
    top: .5em;
    right: .5em;
    font-size: 1.6em;
    opacity: .9;
    line-height: .75
}

.cc-close:focus,
.cc-close:hover {
    opacity: 1
}

.cc-revoke.cc-top {
    top: 0;
    left: 3em;
    border-bottom-left-radius: .5em;
    border-bottom-right-radius: .5em
}

.cc-revoke.cc-bottom {
    bottom: 0;
    left: 3em;
    border-top-left-radius: .5em;
    border-top-right-radius: .5em
}

.cc-revoke.cc-left {
    left: 3em;
    right: unset
}

.cc-revoke.cc-right {
    right: 3em;
    left: unset
}

.cc-top {
    top: 1em
}

.cc-left {
    left: 1em
}

.cc-right {
    right: 1em
}

.cc-bottom {
    bottom: 1em
}

.cc-floating>.cc-link {
    margin-bottom: 1em
}

.cc-floating .cc-message {
    display: block;
    margin-bottom: 1em
}

.cc-window.cc-floating .cc-compliance {
    -ms-flex: 1 0 auto;
    flex: 1 0 auto
}

.cc-window.cc-banner {
    -ms-flex-align: center;
    align-items: center
}

.cc-banner.cc-top {
    left: 0;
    right: 0;
    top: 0
}

.cc-banner.cc-bottom {
    left: 0;
    right: 0;
    bottom: 0
}

.cc-banner .cc-message {
    display: block;
    -ms-flex: 1 1 auto;
    flex: 1 1 auto;
    max-width: 100%;
    margin-right: 1em
}

.cc-compliance {
    display: -ms-flexbox;
    display: flex;
    -ms-flex-align: center;
    align-items: center;
    -ms-flex-line-pack: justify;
    align-content: space-between
}

.cc-floating .cc-compliance>.cc-btn {
    -ms-flex: 1;
    flex: 1
}

.cc-btn+.cc-btn {
    margin-left: .5em
}

@media print {

    .cc-revoke,
    .cc-window {
        display: none
    }
}

@media screen and (max-width:900px) {
    .cc-btn {
        white-space: normal
    }
}

@media screen and (max-width:414px) and (orientation:portrait),
screen and (max-width:736px) and (orientation:landscape) {
    .cc-window{
        margin:0;
    }

    .cc-window.cc-top {
        top: 0
    }

    .cc-window.cc-bottom {
        bottom: 0
    }

    .cc-window.cc-banner,
    .cc-window.cc-floating,
    .cc-window.cc-left,
    .cc-window.cc-right {
        left: 0;
        right: 0
    }

    .cc-window.cc-banner {
        -ms-flex-direction: column;
        flex-direction: column
    }

    .cc-window.cc-banner .cc-compliance {
        -ms-flex: 1 1 auto;
        flex: 1 1 auto
    }

    .cc-window.cc-floating {
        max-width: none
    }

    .cc-window .cc-message {
        margin-bottom: 1em
    }

    .cc-window.cc-banner {
        -ms-flex-align: unset;
        align-items: unset
    }

    .cc-window.cc-banner .cc-message {
        margin-right: 0
    }
}

.cc-floating.cc-theme-classic {
    padding: 1.2em;
    border-radius: 5px
}

.cc-floating.cc-type-info.cc-theme-classic .cc-compliance {
    text-align: center;
    display: inline;
    -ms-flex: none;
    flex: none
}

.cc-theme-classic .cc-btn {
    border-radius: 5px
}

.cc-theme-classic .cc-btn:last-child {
    min-width: 140px
}

.cc-floating.cc-type-info.cc-theme-classic .cc-btn {
    display: inline-block
}

.cc-theme-edgeless.cc-window {
    padding: 0
}

.cc-floating.cc-theme-edgeless .cc-message {
    margin: 2em 2em 1.5em
}

.cc-banner.cc-theme-edgeless .cc-btn {
    margin: 0;
    padding: .8em 1.8em;
    height: 100%
}

.cc-banner.cc-theme-edgeless .cc-message {
    margin-left: 1em
}

.cc-floating.cc-theme-edgeless .cc-btn+.cc-btn {
    margin-left: 0
}
```

Das JS-File solltest Du einfach vom Repo (Ordner:  [build](https://github.com/osano/cookieconsent/tree/dev/build){:target="_blank" rel="nofollow"}  klonen. Falls es hier funktionale Neuerungen gibt, ist besser hier gleich die aktuellste Version zu nutzen.

**Wenn alles geklappt hat, hast Du nun in deiner Jekyll-Instanz eine DSGVO-konforme Cookie-Lösung mit CookieConsent.**

----------

### ein eigener Sache

Bitte prüfe, ob Du wirklich ein Tracking implementierst musst. Verdienst Du Geld mit deiner Webseite? Dann ist es nachvollziehbar und wohl in vielen Fällen aus Marketingsicht gerechtfertigt. Betreibst Du aber nur einen privaten Blog (so wie dieser hier) und setzt keine Trackingtools ein, ist es im Grunde unnötig.  
  
Viele Webseitenbetreiber schreiben diesen tollen Satz „_Wir setzen Cookies, um diese Webseite noch besser zu machen._“ In den meisten Fällen geht es nur um blindes Datensammeln. Tatsächliche datengetriebene Webseiten-Optimierung wird bei den allerwenigsten Betreibern umgesetzt.

### ein letzter Tipp

Mit der DSGVO-konformen Implementierung von CookieConsent hast Du aber bisher nur die halbe Miete. Mit einer ordentlichen Datenschutzerklärung bzw. den Datenschutzhinweisen wird das Ganze erst komplett. Meine Empfehlung:  [Datenschutz-Generator von Dr. Schwenke](https://datenschutz-generator.de/){:target="_blank" rel="nofollow"}
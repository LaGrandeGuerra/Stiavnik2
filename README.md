# Stiavnik2
Stiavnik2
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Štiavnik</title>
<meta name="viewport" content="width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0">
<link rel="stylesheet" type="text/css" href="./Qgis2threejs.css">
<script src="./threejs/three.min.js"></script>
<script src="./threejs/OrbitControls.js"></script>
<script src="./Qgis2threejs.js"></script>
</head>
<body>
<div id="view">
  <div id="labels"></div>
  <div id="northarrow"></div>
</div>

<!-- popup -->
<div id="popup">
  <div id="closebtn">&times;</div>
  <div id="popupbar"></div>
  <div id="popupbody">
    <div id="popupcontent"></div>

    <!-- query result -->
    <div id="queryresult">
      <table id="qr_layername_table">
        <caption>Layer name</caption>
        <tr><td id="qr_layername"></td></tr>
      </table>

      <table id="qr_coords_table">
        <caption>Clicked coordinates</caption>
        <tr><td id="qr_coords"></td></tr>
      </table>

      <!-- camera actions -->
      <div class="action-btn action-zoom" onclick="app.cameraAction.zoomIn(); app.closePopup();">Zoom in here</div>
      <div class="action-btn action-move" onclick="app.cameraAction.move(); app.closePopup();">Move here</div>
      <div class="action-btn action-orbit" onclick="app.cameraAction.orbit(); app.closePopup();">Orbit around here</div>

      <!-- attributes -->
      <table id="qr_attrs_table">
        <caption>Attributes</caption>
      </table>
    </div>

    <!-- page info -->
    <div id="pageinfo">
      <h1>Current View URL</h1>
      <div><input id="urlbox" type="text"></div>

      <h1>Usage</h1>
      <table id="usage">
        <tr><td colspan="2" class="star">Mouse</td></tr>
        <tr><td>Left button + Move</td><td>Orbit</td></tr>
        <tr><td>Mouse Wheel</td><td>Zoom</td></tr>
        <tr><td>Right button + Move</td><td>Pan</td></tr>

        <tr><td colspan="2" class="star">Keys</td></tr>
        <tr><td>Arrow keys</td><td>Move Horizontally</td></tr>
        <tr><td>Shift + Arrow keys</td><td>Orbit</td></tr>
        <tr><td>Ctrl + Arrow keys</td><td>Rotate</td></tr>
        <tr><td>Shift + Ctrl + Up / Down</td><td>Zoom In / Out</td></tr>
        <tr><td>L</td><td>Toggle Label Visibility</td></tr>
        <tr><td>R</td><td>Start / Stop Rotate Animation (Orbiting)</td></tr>
        <tr><td>W</td><td>Wireframe Mode</td></tr>
        <tr><td>Shift + R</td><td>Reset Camera Position</td></tr>
        <tr><td>Shift + S</td><td>Save Image</td></tr>
      </table>

      <h1>About</h1>
      <div id="about">
        This page was made with <a href="https://www.qgis.org/" target="_blank">QGIS</a> and <a href="https://github.com/minorua/Qgis2threejs" target="_blank">Qgis2threejs</a> plugin.
        Dependent JavaScript libraries are
        <a href="https://threejs.org/" target="_blank">three.js</a>
        <span id="lib_proj4js"> and <a href="https://trac.osgeo.org/proj4js/" target="_blank">Proj4js</a></span>
        .
      </div>
    </div>
  </div>
</div>

<!-- progress bar -->
<div id="progress"><div id="bar"></div></div>

<!-- header and footer -->
<div id="header">Majetok cistercitského kláštora v Spišskom Štiavniku a sídla na ňom okolo roku 1320</div>
<div id="footer"><span id="infobtn"><img src="./Qgis2threejs.png"></span> </div>

<script>
Q3D.Config.allVisible = true;
Q3D.Config.localMode = true;
if (typeof proj4 === "undefined") document.getElementById("lib_proj4js").style.display = "none";

var app = Q3D.application,
    container = document.getElementById("view");

app.init(container);           // initialize application

// load the scene
app.loadSceneFile("./data/index/scene.js", function () {
  app.start();

  // North arrow inset
  if (Q3D.Config.northArrow.visible) app.buildNorthArrow(document.getElementById("northarrow"), app.scene.userData.rotation);
});

document.getElementById("infobtn").onclick = app.showInfo.bind(app);
</script>
</body>
</html>

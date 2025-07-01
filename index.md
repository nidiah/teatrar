---
layout: home
title: Base de datos
---

La base de datos del proyecto TeatrAr contiene información sobre obras de teatro producidas en el actual territorio de la República Argentina entre el siglo XVIII y los inicios del siglo XX.

Se ofrece información sobre autoría, fecha y lugar de composición, estreno, género, etc., así como el acceso al texto digital y codificado en XML-TEI y sus visualizaciones desde ArDraCor.

<br>

<table id="tabla-obras" class="display" style="width:100%;">
    <thead>
      <tr>
        <th>Autor</th>
        <th>Título</th>
        <th>Estreno</th>
        <th>Género</th>
      </tr>
    </thead>
    <tbody>
    </tbody>
</table>

  <script>
    Papa.parse("https://docs.google.com/spreadsheets/d/e/2PACX-1vQDRi6oL3EbBS14Z6gOyJc12guLm3_CPOaQ6jDo2CXN9bUCKEJ2dbhmPcvg06Z-pSrZwj4QgfStcjKk/pub?gid=0&single=true&output=csv", {
      download: true,
      header: true,
      complete: function(results) {
        const data = results.data;
        const tbody = $('#tabla-obras tbody');

        data.forEach(row => {
          if (row.Título) { // evitar filas vacías
            const fila = `
              <tr>
                <td>${row.Autor}</td>
                <td><a href="obras/${row.ID}.html">${row.Título}</a></td>
                <td>${row.Estreno}</td>
                <td>${row.Género}</td>
              </tr>`;
            tbody.append(fila);
          }
        });

        $('#tabla-obras').DataTable({
          language: {
            url: '//cdn.datatables.net/plug-ins/1.13.4/i18n/es-ES.json'
          }
        });
      }
    });
  </script>
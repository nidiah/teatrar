---
layout: home
title: Inicio
---

<table id="tabla-obras" class="display" style="width:100%">
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
    Papa.parse("https://docs.google.com/spreadsheets/d/e/2PACX-1vSKUCQc45tMk7W-NkA6R46A0wwl94lGH64vvllB7QaoBZNcn2e9x2wDHsgkmcuny3NAvLBi2J9d2n8v/pub?output=csv", {
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
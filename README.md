<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Coordinación Cuidado Papá</title>
    <style>
      * {
          margin: 0;
          padding: 0;
          box-sizing: border-box;
      }

      body {
          font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
          background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
          min-height: 100vh;
          padding: 20px;
      }

      .container {
          max-width: 1200px;
          margin: 0 auto;
      }

      .header {
          background: white;
          padding: 30px;
          border-radius: 20px;
          box-shadow: 0 10px 40px rgba(0,0,0,0.1);
          margin-bottom: 30px;
      }

      h1 {
          color: #667eea;
          font-size: 28px;
          margin-bottom: 10px;
      }

      .subtitle {
          color: #6b7280;
          font-size: 14px;
      }

      .loading {
          text-align: center;
          padding: 40px;
          color: white;
          font-size: 18px;
      }

      .main-grid {
          display: grid;
          grid-template-columns: 1fr 2fr;
          gap: 20px;
      }

      @media (max-width: 968px) {
          .main-grid {
              grid-template-columns: 1fr;
          }
      }

      .card {
          background: white;
          border-radius: 20px;
          padding: 25px;
          box-shadow: 0 10px 40px rgba(0,0,0,0.1);
      }

      .card-title {
          font-size: 18px;
          font-weight: 600;
          color: #1f2937;
          margin-bottom: 20px;
          display: flex;
          align-items: center;
          gap: 10px;
      }

      .form-group {
          margin-bottom: 15px;
      }

      label {
          display: block;
          color: #4b5563;
          font-size: 13px;
          font-weight: 500;
          margin-bottom: 6px;
      }

      input[type="text"],
      input[type="date"],
      select,
      textarea {
          width: 100%;
          padding: 12px;
          border: 2px solid #e5e7eb;
          border-radius: 10px;
          font-size: 14px;
          transition: all 0.3s;
          font-family: inherit;
      }

      input:focus,
      select:focus,
      textarea:focus {
          outline: none;
          border-color: #667eea;
          box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
      }

      textarea {
          resize: vertical;
          min-height: 80px;
      }

      .checkbox-group {
          display: flex;
          align-items: center;
          gap: 8px;
          margin-bottom: 15px;
      }

      input[type="checkbox"] {
          width: 18px;
          height: 18px;
          cursor: pointer;
      }

      .recurrence-options {
          display: none;
          margin-top: 10px;
          padding: 15px;
          background: #f9fafb;
          border-radius: 10px;
      }

      .recurrence-options.active {
          display: block;
      }

      .btn {
          background: #667eea;
          color: white;
          border: none;
          padding: 12px 24px;
          border-radius: 10px;
          font-size: 14px;
          font-weight: 600;
          cursor: pointer;
          transition: all 0.3s;
          width: 100%;
      }

      .btn:hover {
          background: #5568d3;
          transform: translateY(-2px);
          box-shadow: 0 5px 15px rgba(102, 126, 234, 0.3);
      }

      .btn:disabled {
          background: #9ca3af;
          cursor: not-allowed;
          transform: none;
      }

      .btn-secondary {
          background: #6b7280;
          margin-top: 10px;
      }

      .btn-secondary:hover {
          background: #4b5563;
      }

      .btn-small {
          padding: 6px 12px;
          font-size: 12px;
          width: auto;
      }

      .responsables-list {
          display: flex;
          flex-wrap: wrap;
          gap: 8px;
          margin-bottom: 15px;
      }

      .responsable-tag {
          background: #e0e7ff;
          color: #4338ca;
          padding: 6px 12px;
          border-radius: 20px;
          font-size: 13px;
          display: flex;
          align-items: center;
          gap: 6px;
      }

      .responsable-tag .remove {
          cursor: pointer;
          font-weight: bold;
          color: #4338ca;
      }

      .eventos-list {
          max-height: 600px;
          overflow-y: auto;
      }

      .evento-card {
          background: #f9fafb;
          border-left: 4px solid #667eea;
          padding: 15px;
          margin-bottom: 12px;
          border-radius: 10px;
          cursor: pointer;
          transition: all 0.3s;
      }

      .evento-card:hover {
          transform: translateX(5px);
          box-shadow: 0 5px 15px rgba(0,0,0,0.1);
      }

      .evento-card.recurrent-instance {
          border-left-color: #fbbf24;
      }

      .evento-header {
          display: flex;
          justify-content: space-between;
          align-items: start;
          margin-bottom: 8px;
      }

      .evento-title {
          font-weight: 600;
          color: #1f2937;
          font-size: 15px;
      }

      .evento-date {
          color: #6b7280;
          font-size: 13px;
      }

      .evento-responsable {
          background: #dbeafe;
          color: #1e40af;
          padding: 4px 10px;
          border-radius: 12px;
          font-size: 12px;
          display: inline-block;
          margin-top: 8px;
      }

      .evento-recurrente {
          background: #fef3c7;
          color: #92400e;
          padding: 4px 10px;
          border-radius: 12px;
          font-size: 11px;
          display: inline-block;
          margin-top: 8px;
          margin-left: 5px;
      }

      .evento-origen {
          background: #f3e8ff;
          color: #6b21a8;
          padding: 4px 10px;
          border-radius: 12px;
          font-size: 11px;
          display: inline-block;
          margin-top: 8px;
          margin-left: 5px;
      }

      .filter-bar {
          display: flex;
          gap: 10px;
          margin-bottom: 15px;
          flex-wrap: wrap;
      }

      .filter-bar input,
      .filter-bar select {
          flex: 1;
          min-width: 150px;
      }

      .time-range-buttons {
          display: flex;
          gap: 8px;
          margin-bottom: 15px;
          flex-wrap: wrap;
      }

      .time-range-btn {
          padding: 8px 16px;
          background: #f3f4f6;
          border: 2px solid #e5e7eb;
          border-radius: 8px;
          font-size: 13px;
          cursor: pointer;
          transition: all 0.3s;
          color: #4b5563;
          font-weight: 500;
      }

      .time-range-btn:hover {
          background: #e5e7eb;
      }

      .time-range-btn.active {
          background: #667eea;
          color: white;
          border-color: #667eea;
      }

      .empty-state {
          text-align: center;
          padding: 40px 20px;
          color: #9ca3af;
      }

      .modal {
          display: none;
          position: fixed;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
          background: rgba(0,0,0,0.5);
          z-index: 1000;
          align-items: center;
          justify-content: center;
      }

      .modal.active {
          display: flex;
      }

      .modal-content {
          background: white;
          padding: 30px;
          border-radius: 20px;
          max-width: 500px;
          width: 90%;
          max-height: 90vh;
          overflow-y: auto;
      }

      .modal-header {
          display: flex;
          justify-content: space-between;
          align-items: center;
          margin-bottom: 20px;
      }

      .modal-close {
          cursor: pointer;
          font-size: 24px;
          color: #6b7280;
      }

      .modal-actions {
          display: flex;
          gap: 10px;
          margin-top: 20px;
      }

      .btn-delete {
          background: #ef4444;
      }

      .btn-delete:hover {
          background: #dc2626;
      }

      .stats {
          display: grid;
          grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
          gap: 15px;
          margin-bottom: 20px;
      }

      .stat-card {
          background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
          color: white;
          padding: 20px;
          border-radius: 15px;
          text-align: center;
      }

      .stat-number {
          font-size: 32px;
          font-weight: bold;
          margin-bottom: 5px;
      }

      .stat-label {
          font-size: 13px;
          opacity: 0.9;
      }

      .info-box {
          background: #fef3c7;
          border-left: 4px solid #f59e0b;
          padding: 12px;
          border-radius: 8px;
          font-size: 13px;
          color: #78350f;
          margin-bottom: 15px;
      }

      .sync-indicator {
          position: fixed;
          bottom: 20px;
          right: 20px;
          background: white;
          padding: 10px 20px;
          border-radius: 25px;
          box-shadow: 0 5px 20px rgba(0,0,0,0.2);
          font-size: 13px;
          color: #6b7280;
          display: none;
      }

      .sync-indicator.syncing {
          display: block;
          background: #fef3c7;
          color: #92400e;
      }

      .sync-indicator.success {
          display: block;
          background: #d1fae5;
          color: #065f46;
      }

      .sync-indicator.error {
          display: block;
          background: #fee2e2;
          color: #991b1b;
      }
    </style>
  </head>
  <body>
    <div class="loading" id="loadingScreen">
      <div>⏳ Cargando datos...</div>
    </div>

    <div class="container" id="mainContent" style="display: none;">
      <div class="header">
        <h1>Coordinación Cuidado Papá</h1>
        <p class="subtitle">
          Organiza citas médicas, obligaciones y cuidados • Sincronizado con
          Google Sheets
        </p>
      </div>

      <div class="stats" id="stats">
        <div class="stat-card">
          <div class="stat-number" id="totalEventos">0</div>
          <div class="stat-label">Total Eventos</div>
        </div>
        <div class="stat-card">
          <div class="stat-number" id="proximosEventos">0</div>
          <div class="stat-label">Próximos 7 días</div>
        </div>
      </div>

      <div class="main-grid">
        <!-- Formulario -->
        <div class="card">
          <div class="card-title">➕ Nuevo Evento</div>

          <div class="form-group">
            <label>Responsables</label>
            <div class="responsables-list" id="responsablesList"></div>
            <input
              type="text"
              id="nuevoResponsable"
              placeholder="Nombre del responsable"
            />
            <button
              class="btn btn-secondary btn-small"
              onclick="agregarResponsable()"
            >
              + Responsable
            </button>
          </div>

          <form id="eventoForm" onsubmit="agregarEvento(event)">
            <div class="form-group">
              <label>Descripción del Evento</label>
              <textarea
                id="descripcion"
                required
                placeholder="Ej: Cita con cardiólogo, Pago seguro médico"
              ></textarea>
            </div>

            <div class="form-group">
              <label>Fecha</label>
              <input type="date" id="fecha" required />
            </div>

            <div class="form-group">
              <label>Hora</label>
              <select id="hora">
                <option value="">Sin hora específica</option>
              </select>
            </div>

            <div class="form-group">
              <label>Responsable</label>
              <select id="responsable" required>
                <option value="">Seleccionar...</option>
              </select>
            </div>

            <div class="checkbox-group">
              <input
                type="checkbox"
                id="recurrente"
                onchange="toggleRecurrencia()"
              />
              <label for="recurrente" style="margin: 0;"
                >Evento recurrente</label
              >
            </div>

            <div class="recurrence-options" id="recurrenceOptions">
              <div class="info-box">
                ℹ️ Se generarán eventos para los próximos 365 días según la
                frecuencia seleccionada
              </div>
              <div class="form-group">
                <label>Frecuencia</label>
                <select id="frecuencia">
                  <option value="diario">Diario</option>
                  <option value="semanal">Semanal</option>
                  <option value="mensual">Mensual</option>
                </select>
              </div>
            </div>

            <button type="submit" class="btn" id="submitBtn">
              Agregar Evento
            </button>
          </form>
        </div>

        <!-- Lista de Eventos -->
        <div class="card">
          <div class="card-title">📅 Eventos Programados</div>

          <div class="time-range-buttons">
            <button
              class="time-range-btn active"
              onclick="setTimeRange('all', this)"
            >
              Todos
            </button>
            <button class="time-range-btn" onclick="setTimeRange(7, this)">
              7 días
            </button>
            <button class="time-range-btn" onclick="setTimeRange(30, this)">
              30 días
            </button>
            <button class="time-range-btn" onclick="setTimeRange(90, this)">
              3 meses
            </button>
            <button class="time-range-btn" onclick="setTimeRange(180, this)">
              6 meses
            </button>
            <button class="time-range-btn" onclick="setTimeRange(365, this)">
              1 año
            </button>
          </div>

          <div class="filter-bar">
            <input
              type="text"
              id="searchEvento"
              placeholder="🔍 Buscar..."
              oninput="filtrarEventos()"
            />
            <select id="filterResponsable" onchange="filtrarEventos()">
              <option value="">Todos los responsables</option>
            </select>
            <button class="btn btn-small" onclick="cargarDatos()">
              🔄 Recargar
            </button>
          </div>

          <div class="eventos-list" id="eventosList">
            <div class="empty-state">
              <p>No hay eventos programados</p>
              <p style="font-size: 12px; margin-top: 8px;">
                Agrega el primer evento para comenzar
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal de Edición -->
    <div class="modal" id="editModal">
      <div class="modal-content">
        <div class="modal-header">
          <h2 style="color: #667eea;">Editar Evento</h2>
          <span class="modal-close" onclick="cerrarModal()">×</span>
        </div>

        <form id="editForm" onsubmit="guardarEdicion(event)">
          <input type="hidden" id="editId" />

          <div class="form-group">
            <label>Descripción</label>
            <textarea id="editDescripcion" required></textarea>
          </div>

          <div class="form-group">
            <label>Fecha</label>
            <input type="date" id="editFecha" required />
          </div>

          <div class="form-group">
            <label>Hora</label>
            <select id="editHora">
              <option value="">Sin hora específica</option>
            </select>
          </div>

          <div class="form-group">
            <label>Responsable</label>
            <select id="editResponsable" required></select>
          </div>

          <div id="editRecurrentInfo" style="display: none;" class="info-box">
            ℹ️ Este evento fue generado automáticamente. Los cambios solo
            afectarán esta instancia.
          </div>

          <div class="modal-actions">
            <button type="submit" class="btn" style="flex: 1;">
              Guardar Cambios
            </button>
            <button
              type="button"
              class="btn btn-delete"
              style="flex: 1;"
              onclick="eliminarEvento()"
            >
              Eliminar
            </button>
          </div>
        </form>
      </div>
    </div>

    <div class="sync-indicator" id="syncIndicator"></div>

    <script>
          // ⚠️ IMPORTANTE: Reemplaza esta URL con la URL de tu Apps Script
          const SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbwoSy-iKNlNUYngxQZv7hu_aAhTCJ6Nf0gsYm52ET_ictMOkOQ4QYbDOv90djrbdNZoSg/exec';

          let responsables = [];
          let eventos = [];
          let eventoEditando = null;
          let currentTimeRange = 'all';

          // Mostrar indicador de sincronización
          function mostrarSync(tipo, mensaje) {
              const indicator = document.getElementById('syncIndicator');
              indicator.className = `sync-indicator ${tipo}`;
              indicator.textContent = mensaje;

              if (tipo === 'success' || tipo === 'error') {
                  setTimeout(() => {
                      indicator.style.display = 'none';
                  }, 3000);
              }
          }

          // Llamadas a la API
          async function apiCall(action, params = {}) {
              mostrarSync('syncing', '⏳ Sincronizando...');

              try {
                  const url = new URL(SCRIPT_URL);
                  url.searchParams.append('action', action);

                  Object.keys(params).forEach(key => {
                      url.searchParams.append(key, params[key]);
                  });

                  const response = await fetch(url);
                  const data = await response.json();

                  mostrarSync('success', '✓ Sincronizado');
                  return data;
              } catch (error) {
                  console.error('Error en API:', error);
                  mostrarSync('error', '✗ Error de conexión');
                  throw error;
              }
          }

          // Generar opciones de hora
          function generarOpcionesHora() {
              const selects = [document.getElementById('hora'), document.getElementById('editHora')];

              selects.forEach(select => {
                  const sinHoraOption = select.querySelector('option[value=""]');
                  select.innerHTML = '';
                  select.appendChild(sinHoraOption.cloneNode(true));

                  for (let h = 0; h < 24; h++) {
                      for (let m = 0; m < 60; m += 5) {
                          const hora = String(h).padStart(2, '0');
                          const minuto = String(m).padStart(2, '0');
                          const valor = `${hora}:${minuto}`;
                          const option = document.createElement('option');
                          option.value = valor;
                          option.textContent = valor;
                          select.appendChild(option);
                      }
                  }
              });
          }

          // Cargar datos
          async function cargarDatos() {
              try {
                  const [respData, eventData] = await Promise.all([
                      apiCall('getResponsables'),
                      apiCall('getEventos')
                  ]);

                  responsables = respData.responsables || [];
                  eventos = eventData.eventos || [];

                  actualizarResponsables();
                  renderizarEventos();
                  actualizarEstadisticas();

                  document.getElementById('loadingScreen').style.display = 'none';
                  document.getElementById('mainContent').style.display = 'block';
              } catch (error) {
                  document.getElementById('loadingScreen').innerHTML =
                      '<div style="color: #ef4444;">❌ Error al cargar datos. Verifica la configuración.</div>';
              }
          }

          // Agregar responsable
          async function agregarResponsable() {
              const input = document.getElementById('nuevoResponsable');
              const nombre = input.value.trim();

              if (nombre && !responsables.includes(nombre)) {
                  await apiCall('addResponsable', { nombre });
                  input.value = '';
                  await cargarDatos();
              }
          }

          // Actualizar lista de responsables
          function actualizarResponsables() {
              const listContainer = document.getElementById('responsablesList');
              const select = document.getElementById('responsable');
              const editSelect = document.getElementById('editResponsable');
              const filterSelect = document.getElementById('filterResponsable');

              // Lista visual
              listContainer.innerHTML = responsables.map(r =>
                  `<div class="responsable-tag">
                      ${r}
                      <span class="remove" onclick="eliminarResponsable('${r}')">×</span>
                  </div>`
              ).join('');

              // Actualizar selects
              const options = responsables.map(r => `<option value="${r}">${r}</option>`).join('');
              select.innerHTML = '<option value="">Seleccionar...</option>' + options;
              editSelect.innerHTML = '<option value="">Seleccionar...</option>' + options;
              filterSelect.innerHTML = '<option value="">Todos los responsables</option>' + options;
          }

          // Eliminar responsable
          async function eliminarResponsable(nombre) {
              if (confirm(`¿Eliminar responsable "${nombre}"?`)) {
                  await apiCall('deleteResponsable', { nombre });
                  await cargarDatos();
              }
          }

          // Toggle recurrencia
          function toggleRecurrencia() {
              const checkbox = document.getElementById('recurrente');
              const options = document.getElementById('recurrenceOptions');
              options.classList.toggle('active', checkbox.checked);
          }

          // Generar eventos recurrentes
          function generarEventosRecurrentes(eventoBase) {
              const eventos = [];
              const fechaInicio = new Date(eventoBase.fecha + 'T00:00:00');
              const fechaLimite = new Date(fechaInicio);
              fechaLimite.setDate(fechaLimite.getDate() + 365);

              let fechaActual = new Date(fechaInicio);

              while (fechaActual <= fechaLimite) {
                  const evento = {
                      id: Date.now() + Math.random(),
                      descripcion: eventoBase.descripcion,
                      fecha: fechaActual.toISOString().split('T')[0],
                      hora: eventoBase.hora,
                      responsable: eventoBase.responsable,
                      recurrente: true,
                      frecuencia: eventoBase.frecuencia,
                      eventoOrigenId: eventoBase.id,
                      fechaOrigen: eventoBase.fecha
                  };

                  eventos.push(evento);

                  if (eventoBase.frecuencia === 'diario') {
                      fechaActual.setDate(fechaActual.getDate() + 1);
                  } else if (eventoBase.frecuencia === 'semanal') {
                      fechaActual.setDate(fechaActual.getDate() + 7);
                  } else if (eventoBase.frecuencia === 'mensual') {
                      fechaActual.setMonth(fechaActual.getMonth() + 1);
                  }
              }

              return eventos;
          }

          // Agregar evento
          async function agregarEvento(e) {
              e.preventDefault();

              const submitBtn = document.getElementById('submitBtn');
              submitBtn.disabled = true;
              submitBtn.textContent = 'Guardando...';

              try {
                  const esRecurrente = document.getElementById('recurrente').checked;

                  const eventoBase = {
                      id: Date.now(),
                      descripcion: document.getElementById('descripcion').value,
                      fecha: document.getElementById('fecha').value,
                      hora: document.getElementById('hora').value,
                      responsable: document.getElementById('responsable').value,
                      recurrente: esRecurrente,
                      frecuencia: esRecurrente ? document.getElementById('frecuencia').value : ''
                  };

                  let eventosAGuardar = [];

                  if (esRecurrente) {
                      eventosAGuardar = generarEventosRecurrentes(eventoBase);
                  } else {
                      eventosAGuardar = [eventoBase];
                  }

                  // Guardar todos los eventos
                  for (const evento of eventosAGuardar) {
                      await apiCall('addEvento', {
                          id: evento.id,
                          descripcion: evento.descripcion,
                          fecha: evento.fecha,
                          hora: evento.hora,
                          responsable: evento.responsable,
                          recurrente: evento.recurrente,
                          frecuencia: evento.frecuencia || '',
                          eventoOrigenId: evento.eventoOrigenId || '',
                          fechaOrigen: evento.fechaOrigen || ''
                      });
                  }

                  document.getElementById('eventoForm').reset();
                  document.getElementById('recurrenceOptions').classList.remove('active');

                  await cargarDatos();
              } catch (error) {
                  alert('Error al guardar evento');
              } finally {
                  submitBtn.disabled = false;
                  submitBtn.textContent = 'Agregar Evento';
              }
          }

          // Establecer rango de tiempo
          function setTimeRange(range, btnElement) {
          currentTimeRange = range;
          document.querySelectorAll('.time-range-btn').forEach(btn => {
              btn.classList.remove('active');
          });
          btnElement.classList.add('active');
          filtrarEventos();
      }

          // Renderizar eventos
          function renderizarEventos() {
              const container = document.getElementById('eventosList');
              const searchTerm = document.getElementById('searchEvento').value.toLowerCase();
              const filterResp = document.getElementById('filterResponsable').value;

              let eventosFiltrados = eventos.filter(e => {
                  const matchSearch = e.descripcion.toLowerCase().includes(searchTerm);
                  const matchResp = !filterResp || e.responsable === filterResp;

                  if (currentTimeRange !== 'all') {
                      const fechaEvento = new Date(e.fecha + 'T00:00:00');
                      const hoy = new Date();
                      hoy.setHours(0, 0, 0, 0);
                      const fechaLimite = new Date(hoy);
                      fechaLimite.setDate(fechaLimite.getDate() + currentTimeRange);

                      if (fechaEvento < hoy || fechaEvento > fechaLimite) {
                          return false;
                      }
                  }

                  return matchSearch && matchResp;
              });

              if (eventosFiltrados.length === 0) {
                  container.innerHTML = '<div class="empty-state"><p>No hay eventos que coincidan</p></div>';
                  return;
              }

              container.innerHTML = eventosFiltrados.map(e => {
                  const fecha = new Date(e.fecha + 'T00:00:00');
                  const fechaFormateada = fecha.toLocaleDateString('es-CL', {
                      weekday: 'short',
                      day: 'numeric',
                      month: 'short',
                      year: 'numeric'
                  });

                  const cardClass = e.eventoOrigenId ? 'evento-card recurrent-instance' : 'evento-card';

                  return `
                      <div class="${cardClass}" onclick="editarEvento(${e.id})">
                          <div class="evento-header">
                              <div>
                                  <div class="evento-title">${e.descripcion}</div>
                                  <div class="evento-date">📅 ${fechaFormateada} ${e.hora ? '• ⏰ ' + e.hora : ''}</div>
                              </div>
                          </div>
                          <span class="evento-responsable">👤 ${e.responsable}</span>
                          ${e.recurrente && !e.eventoOrigenId ? `<span class="evento-recurrente">🔁 ${e.frecuencia}</span>` : ''}
                          ${e.eventoOrigenId ? `<span class="evento-origen">🔗 Origen: ${new Date(e.fechaOrigen + 'T00:00:00').toLocaleDateString('es-CL', {day: 'numeric', month: 'short'})}</span>` : ''}
                      </div>
                  `;
              }).join('');
          }

          // Filtrar eventos
          function filtrarEventos() {
              renderizarEventos();
          }

          // Editar evento
          function editarEvento(id) {
              eventoEditando = eventos.find(e => e.id === id);
              if (!eventoEditando) return;

              document.getElementById('editId').value = eventoEditando.id;
              document.getElementById('editDescripcion').value = eventoEditando.descripcion;
              document.getElementById('editFecha').value = eventoEditando.fecha;
              document.getElementById('editHora').value = eventoEditando.hora || '';
              document.getElementById('editResponsable').value = eventoEditando.responsable;

              const infoBox = document.getElementById('editRecurrentInfo');
              if (eventoEditando.eventoOrigenId) {
                  infoBox.style.display = 'block';
              } else {
                  infoBox.style.display = 'none';
              }

              document.getElementById('editModal').classList.add('active');
          }

          // Guardar edición
          async function guardarEdicion(e) {
              e.preventDefault();

              try {
                  await apiCall('updateEvento', {
                      id: document.getElementById('editId').value,
                      descripcion: document.getElementById('editDescripcion').value,
                      fecha: document.getElementById('editFecha').value,
                      hora: document.getElementById('editHora').value,
                      responsable: document.getElementById('editResponsable').value
                  });

                  await cargarDatos();
                  cerrarModal();
              } catch (error) {
                  alert('Error al guardar cambios');
              }
          }

          // Eliminar evento
          async function eliminarEvento() {
              if (confirm('¿Eliminar este evento?')) {
                  try {
                      await apiCall('deleteEvento', {
                          id: document.getElementById('editId').value
                      });

                      await cargarDatos();
                      cerrarModal();
                  } catch (error) {
                      alert('Error al eliminar evento');
                  }
              }
          }

          // Cerrar modal
          function cerrarModal() {
              document.getElementById('editModal').classList.remove('active');
              eventoEditando = null;
          }

          // Actualizar estadísticas
          function actualizarEstadisticas() {
              document.getElementById('totalEventos').textContent = eventos.length;

              const hoy = new Date();
              hoy.setHours(0, 0, 0, 0);
              const enSieteDias = new Date(hoy);
              enSieteDias.setDate(enSieteDias.getDate() + 7);

              const proximos = eventos.filter(e => {
                  const fechaEvento = new Date(e.fecha + 'T00:00:00');
                  return fechaEvento >= hoy && fechaEvento <= enSieteDias;
              });

              document.getElementById('proximosEventos').textContent = proximos.length;
          }

          // Inicializar
          document.addEventListener('DOMContentLoaded', () => {
              generarOpcionesHora();
              cargarDatos();

              const hoy = new Date().toISOString().split('T')[0];
              document.getElementById('fecha').value = hoy;
          });

          document.getElementById('editModal').addEventListener('click', (e) => {
              if (e.target.id === 'editModal') {
                  cerrarModal();
              }
          });
    </script>
  </body>
</html>

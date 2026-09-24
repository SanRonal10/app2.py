import streamlit as st
import pandas as pd
import plotly.express as px

# Configuración de página
st.set_page_config(
    page_title="Ruta de Aprendizaje SAP Business One HANA",
    page_icon="💼",
    layout="wide",
    initial_sidebar_state="expanded"
)

# Estilos CSS personalizados para mejorar el diseño
st.markdown("""
<style>
    .main-header {
        font-size: 2.2rem;
        font-weight: 700;
        color: #0F172A;
        margin-bottom: 0.5rem;
    }
    .sub-header {
        font-size: 1.1rem;
        color: #475569;
        margin-bottom: 2rem;
    }
    .card {
        background-color: #F8FAFC;
        border: 1px solid #E2E8F0;
        border-radius: 10px;
        padding: 1.2rem;
        margin-bottom: 1rem;
    }
    .stProgress > div > div > div > div {
        background-color: #0284C7;
    }
</style>
""", unsafe_allow_html=True)

# -----------------------------------------------------------------------------
# SIDEBAR / PANEL LATERAL
# -----------------------------------------------------------------------------
st.sidebar.image("https://upload.wikimedia.org/wikipedia/commons/5/59/SAP_2011_logo.svg", width=120)
st.sidebar.title("Navegación")

opcion_menu = st.sidebar.radio(
    "Selecciona una sección:",
    ["🛣️ Ruta de Aprendizaje", "📚 Cursos Recomendados", "📊 Evaluador de Perfil", "📜 Certificación SAP"]
)

st.sidebar.markdown("---")
st.sidebar.subheader("🎯 Configuración de Perfil")
perfil_objetivo = st.sidebar.selectbox(
    "Tu objetivo profesional:",
    ["Consultor Funcional", "Consultor Técnico / Desarrollador", "Consultor Integral / Solution Architect"]
)

st.sidebar.info("💡 **Consejo:** La combinación de habilidades técnicas (SQL/HANA, Service Layer) y conocimiento funcional financiero incrementa el valor de un consultor SAP B1.")

# -----------------------------------------------------------------------------
# SECCIÓN 1: RUTA DE APRENDIZAJE
# -----------------------------------------------------------------------------
if opcion_menu == "🛣️ Ruta de Aprendizaje":
    st.markdown("<div class='main-header'>Ruta de Aprendizaje: SAP Business One on HANA</div>", unsafe_allow_html=True)
    st.markdown(f"<div class='sub-header'>Plan estructurado paso a paso para el perfil: <b>{perfil_objetivo}</b></div>", unsafe_allow_html=True)

    # Métricas principales
    col1, col2, col3, col4 = st.columns(4)
    col1.metric("Duración Estimada", "6 - 9 meses", "Ritmo flexible")
    col2.metric("Módulos Clave", "8 Módulos", "Funcional + Técnico")
    col3.metric("Base de Datos", "SAP HANA 2.0", "In-Memory Engine")
    col4.metric("Certificación", "C_TB1200", "Examen Oficial")

    st.markdown("---")

    # Contenido de la Ruta en Pestañas
    tab1, tab2, tab3, tab4, tab5 = st.tabs([
        "Fase 1: Fundamentos ERP", 
        "Fase 2: Motor SAP HANA", 
        "Fase 3: Desarrollo & APIs", 
        "Fase 4: Analítica & SIRE", 
        "Fase 5: Metodología"
    ])

    with tab1:
        st.subheader("1. Procesos de Negocio en SAP Business One")
        st.write("Comprensión integral de los flujos logísticos y financieros del ERP.")
        
        c1, c2 = st.columns(2)
        with c1:
            st.markdown("""
            * **Módulo de Compras (P2P):** Solicitud -> Oferta -> Orden -> Entrada de Mercancía -> Factura de Proveedores.
            * **Módulo de Ventas (O2C):** Cotización -> Orden -> Entrega -> Factura de Deudores -> Cobro.
            * **Gestión de Inventarios:** Valoración (FIFO, Promedio Ponderado, Estándar), Traslados, Revalorizaciones y Recuentos.
            """)
        with c2:
            st.markdown("""
            * **Finanzas y Contabilidad:** Plan de Cuentas, Asientos Contables, Centros de Costo, Dimensiones y Contabilidad Analítica.
            * **Bancos y Pagos:** Pagos recibidos, pagos efectuados y reconciliaciones bancarias.
            """)
        
        st.code("Código Oficial SAP: TB1000 (SAP Business One - Logistics & Financials)", language="text")

    with tab2:
        st.subheader("2. Arquitectura y Modelado en SAP HANA")
        st.write("Explotación técnica del motor in-memory de SAP HANA Studio.")
        
        st.markdown("""
        * **Consultas SQL en HANA:** Dominio de `SELECT`, `JOIN`, subconsultas y funciones avanzadas en sintaxis HANA SQL.
        * **Modelado Analítico:** Creación de *Calculation Views* (Graphical y Scripted) para consolidación de datos.
        * **Vistas de Base de Datos:** Vistas de sistema (`OINV`, `INV1`, `OCRD`, `OITM`) y tablas del sistema.
        * **Lógica de Negocio en BD:** Creación de Stored Procedures y `TransactionNotification` para validaciones en tiempo real.
        """)
        
        st.info("📌 **Tip Técnico:** En HANA Studio, asegúrate de optimizar el uso de filtros y proyecciones en las *Calculation Views* antes de realizar agregaciones.")

    with tab3:
        st.subheader("3. Desarrollo de Add-ons y Consumo de APIs")
        st.write("Extensión y personalización del ERP para requerimientos específicos.")
        
        c1, c2 = st.columns(2)
        with c1:
            st.markdown("#### Service Layer (REST API)")
            st.markdown("""
            * Arquitectura basada en OData v4.
            * Operaciones CRUD vía Postman / Python / C#.
            * Manejo de autenticación, B1S-Session y endpoints nativos.
            """)
        with c2:
            st.markdown("#### SDK Tradicional (UI/DI API)")
            st.markdown("""
            * **DI API:** Manipulación de objetos de negocio mediante código C#.
            * **UI API:** Creación de formularios personalizados e interceptación de eventos en el cliente nativo.
            """)

    with tab4:
        st.subheader("4. Analítica de Datos y Localización Fiscal")
        st.markdown("""
        * **Dashboard Designer y Pervasive Analytics:** Creación de KPIs, Dashboards y Widget Analtyics dentro de SAP B1 HANA.
        * **Integración Power BI:** Conexión mediante conectores ODBC/ODBC HANA o peticiones al Service Layer.
        * **Integración Fiscal:** Desarrollo de estructuras TXT y consultas SQL para reportes regulatorios (e.g., SUNAT SIRE).
        """)

    with tab5:
        st.subheader("5. Metodología de Implementación")
        st.markdown("""
        * **Metodología Accelerated SAP (ASAP) / SAP Activate:**
          1. Preparación del Proyecto.
          2. Plano de Negocio (Business Blueprint - BBP).
          3. Realización (Configuración y migración con DTW - Data Transfer Workbench).
          4. Preparación Final (Capacitación y Pruebas UAT).
          5. Golive y Soporte Post-Implementación.
        """)

# -----------------------------------------------------------------------------
# SECCIÓN 2: CURSOS RECOMENDADOS
# -----------------------------------------------------------------------------
elif opcion_menu == "📚 Cursos Recomendados":
    st.markdown("<div class='main-header'>Catálogo de Cursos y Formación</div>", unsafe_allow_html=True)
    st.markdown("<div class='sub-header'>Ruta de cursos oficiales y complementarios sugeridos para dominar el ecosistema.</div>", unsafe_allow_html=True)

    cursos = [
        {
            "nombre": "TB1000 - SAP Business One Logistics",
            "tipo": "Oficial SAP",
            "nivel": "Principiante - Intermedio",
            "duración": "40 hrs",
            "descripcion": "Cubre todos los flujos logísticos, ventas, compras e inventario en SAP Business One."
        },
        {
            "nombre": "TB1100 - SAP Business One Accounting",
            "tipo": "Oficial SAP",
            "nivel": "Intermedio",
            "duración": "30 hrs",
            "descripcion": "Gestión financiera, contabilidad general, activos fijos, bancos y cierres de periodo."
        },
        {
            "nombre": "TB1200 - SAP Business One Implementation & Administration",
            "tipo": "Oficial SAP",
            "nivel": "Avanzado",
            "duración": "40 hrs",
            "descripcion": "Curso clave para la certificación oficial. Cubre parametrización, DTW, permisos y configuración global."
        },
        {
            "nombre": "SAP HANA Modeling & SQL Scripting",
            "tipo": "Técnico / Especialización",
            "nivel": "Intermedio - Avanzado",
            "duración": "25 hrs",
            "descripcion": "Modelado de Calculation Views, procedimientos almacenados y optimización de consultas en HANA Studio."
        },
        {
            "nombre": "Desarrollo con SAP Business One Service Layer (OData/REST)",
            "tipo": "Técnico",
            "nivel": "Avanzado",
            "duración": "20 hrs",
            "descripcion": "Integración de sistemas externos, desarrollo de portales web y apps móviles consumiendo el Service Layer."
        }
    ]

    for curso in cursos:
        with st.expander(f"📖 {curso['nombre']}  |  [{curso['tipo']}]"):
            c1, c2 = st.columns([3, 1])
            with c1:
                st.write(curso["descripcion"])
            with c2:
                st.caption(f"**Nivel:** {curso['nivel']}")
                st.caption(f"**Duración:** {curso['duración']}")

# -----------------------------------------------------------------------------
# SECCIÓN 3: EVALUADOR DE PERFIL
# -----------------------------------------------------------------------------
elif opcion_menu == "📊 Evaluador de Perfil":
    st.markdown("<div class='main-header'>Evaluador de Preparación para Consultores</div>", unsafe_allow_html=True)
    st.markdown("<div class='sub-header'>Evalúa tu nivel actual para identificar áreas de mejora hacia tu perfil deseado.</div>", unsafe_allow_html=True)

    st.write("Responde las siguientes preguntas indicando tu grado de dominio:")

    q1 = st.slider("1. Dominio de flujos de Compras y Ventas en SAP B1", 0, 10, 5)
    q2 = st.slider("2. Conocimiento de Finanzas, Plan de Cuentas y Contabilidad Analítica", 0, 10, 4)
    q3 = st.slider("3. Habilidad escribiendo consultas SQL y objetos en SAP HANA Studio", 0, 10, 6)
    q4 = st.slider("4. Experiencia con Service Layer, APIs REST o desarrollo de Add-ons", 0, 10, 3)
    q5 = st.slider("5. Manejo de migración de datos con DTW (Data Transfer Workbench)", 0, 10, 5)

    score_total = (q1 + q2 + q3 + q4 + q5) * 2  # Porcentaje sobre 100

    st.markdown("---")
    st.subheader("Resultado de tu Evaluación")
    
    col_score, col_chart = st.columns([1, 2])

    with col_score:
        st.metric("Puntuación Global", f"{score_total}%")
        if score_total >= 80:
            st.success("🎉 **Nivel Avanzado / Senior:** Estás preparado para liderar proyectos de implementación y desarrollo en SAP B1 HANA.")
        elif score_total >= 50:
            st.warning("📈 **Nivel Intermedio:** Tienes bases sólidas. Enfócate en profundizar en las áreas técnicas o financieras según tu meta.")
        else:
            st.error("🚀 **Nivel Junior / En Formación:** Te recomendamos iniciar con los módulos TB1000 y prácticas con SQL en HANA.")

    with col_chart:
        df_chart = pd.DataFrame({
            "Área": ["Logística", "Finanzas", "HANA SQL", "APIs/Addons", "Migración DTW"],
            "Puntaje": [q1, q2, q3, q4, q5]
        })
        fig = px.line_polar(df_chart, r='Puntaje', theta='Área', line_close=True, range_r=[0, 10])
        fig.update_traces(fill='toself', line_color='#0284C7')
        fig.update_layout(margin=dict(l=20, r=20, t=20, b=20), height=250)
        st.plotly_chart(fig, use_container_width=True)

# -----------------------------------------------------------------------------
# SECCIÓN 4: CERTIFICACIÓN
# -----------------------------------------------------------------------------
elif opcion_menu == "📜 Certificación SAP":
    st.markdown("<div class='main-header'>Certificación Oficial SAP Business One</div>", unsafe_allow_html=True)
    st.markdown("<div class='sub-header'>Guía de preparación para el examen oficial de certificación.</div>", unsafe_allow_html=True)

    st.markdown("""
    <div class='card'>
        <h3>Examen de Certificación: C_TB1200</h3>
        <p><b>Nombre oficial:</b> SAP Certified Application Associate - SAP Business One Release 10.0</p>
        <ul>
            <li><b>Número de preguntas:</b> 80 preguntas de opción múltiple.</li>
            <li><b>Puntaje de aprobación:</b> ~65% (varía según versión).</li>
            <li><b>Duración:</b> 180 minutos.</li>
            <li><b>Idioma:</b> Inglés / Español (según disponibilidad del centro).</li>
        </ul>
    </div>
    """, unsafe_allow_html=True)

    st.subheader("Desglose de Temas del Examen")
    
    df_cert = pd.DataFrame({
        "Tema principal": ["Logistics & Sales", "Financials & Accounting", "Configuration & Customization", "Implementation Methodology", "Reporting & Analytics"],
        "Ponderación aproximada": ["30%", "25%", "20%", "15%", "10%"]
    })
    st.table(df_cert)

    st.success("💡 **Estrategia de Estudio:** Estudia a fondo los manuales **TB1000, TB1100 y TB1200**. Realiza prácticas reales en un ambiente de pruebas (*Sandbox*) creando sociedades desde cero y simulando migraciones.")

# Pie de página
st.markdown("---")
st.caption("Desarrollado para la comunidad de consultores SAP Business One on HANA | Listo para desplegar en Streamlit Cloud.")

# Dashboard Design System

> **Назначение:** Глобальная дизайн-система для всех дашбордов. Применяется автоматически при создании любых BI-дашбордов, прототипов аналитики, визуализаций.
>
> **Триггер:** Ключевые слова в запросе: "дашборд", "dashboard", "визуализация", "графики", "аналитика", "BI", "metrics".
>
> **Приоритет:** Эти правила ВСЕГДА имеют приоритет над дефолтными преднастройками AI-агента.

---

## Цветовая палитра

### Философия
**Тема:** Здоровье · Успех · Экология · Нейтральность · Баланс

**Избегать:**
- ❌ Фиолетовые оттенки (#8B5CF6, #A855F7, #C084FC)
- ❌ Неоновые цвета
- ❌ Кислотные оттенки

### Основная палитра

```python
BRAND_COLORS = {
    # Primary: Природный зеленый (успех, рост, стабильность)
    'primary': '#059669',      # Emerald-600
    'primary_light': '#10B981', # Emerald-500
    'primary_dark': '#047857',  # Emerald-700
    
    # Secondary: Небесный синий (доверие, спокойствие, аналитика)
    'secondary': '#0284C7',     # Sky-600
    'secondary_light': '#0EA5E9', # Sky-500
    'secondary_dark': '#0369A1', # Sky-700
    
    # Accent: Теплый янтарь (внимание, важность)
    'accent': '#D97706',        # Amber-600
    'accent_light': '#F59E0B',  # Amber-500
    
    # Status colors
    'success': '#059669',       # Emerald-600
    'warning': '#D97706',       # Amber-600
    'danger': '#DC2626',        # Red-600
    'info': '#0284C7',          # Sky-600
    
    # Neutrals (компактность: приглушенные тона)
    'text_primary': '#1F2937',   # Gray-800
    'text_secondary': '#6B7280', # Gray-500
    'border': '#D1D5DB',         # Gray-300
    'background': '#F9FAFB',     # Gray-50
    'surface': '#FFFFFF',
}
```

### Палитры для графиков

**10-цветная палитра** (для categorical data):
```python
CHART_PALETTE_10 = [
    '#059669',  # Emerald-600 — основной
    '#0284C7',  # Sky-600 — вторичный
    '#D97706',  # Amber-600 — акцент
    '#06B6D4',  # Cyan-500 — свежесть
    '#10B981',  # Emerald-500 — светлый успех
    '#0EA5E9',  # Sky-500 — светлое небо
    '#84CC16',  # Lime-500 — эко
    '#14B8A6',  # Teal-500 — морской
    '#22C55E',  # Green-500 — природа
    '#6B7280',  # Gray-500 — нейтраль (для "Остальные")
]
```

**Градиенты** (3-4 цвета):
```python
GRADIENTS = {
    'success': ['#047857', '#059669', '#10B981', '#34D399'],  # темный → светлый зеленый
    'info': ['#0369A1', '#0284C7', '#0EA5E9', '#38BDF8'],     # темный → светлый синий
    'warm': ['#D97706', '#F59E0B', '#FBBF24', '#FCD34D'],     # темный → светлый янтарь
    'eco': ['#065F46', '#059669', '#10B981', '#6EE7B7'],      # темный изумруд → мятный
}
```

---

## Типографика

```python
TYPOGRAPHY = {
    'font_family': "'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif",
    'font_family_mono': "'JetBrains Mono', 'Fira Code', 'Consolas', monospace",
    
    # Sizes (компактность: уменьшены на 10-15% от стандарта)
    'h1': {'size': '2rem', 'weight': 600, 'line_height': 1.2},      # 32px
    'h2': {'size': '1.5rem', 'weight': 600, 'line_height': 1.3},    # 24px
    'h3': {'size': '1.25rem', 'weight': 600, 'line_height': 1.4},   # 20px
    'body': {'size': '0.875rem', 'weight': 400, 'line_height': 1.5}, # 14px
    'small': {'size': '0.75rem', 'weight': 400, 'line_height': 1.4}, # 12px
    'metric': {'size': '1.75rem', 'weight': 700, 'line_height': 1},  # 28px для чисел
}
```

**Google Fonts импорт:**
```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
```

---

## Spacing System (компактность)

**Базовая единица:** 4px

```python
SPACING = {
    'xs': '0.25rem',   # 4px
    'sm': '0.5rem',    # 8px
    'md': '0.75rem',   # 12px (вместо стандартных 16px)
    'lg': '1rem',      # 16px (вместо 24px)
    'xl': '1.5rem',    # 24px (вместо 32px)
    '2xl': '2rem',     # 32px
}
```

**Применение:**
- Padding внутри карточек: `md` (12px)
- Gap между элементами: `sm` (8px)
- Margin между секциями: `lg` (16px)
- Margin между группами: `xl` (24px)

---

## Визуальные эффекты

### Тени (минималистичные)
```css
box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);         /* card */
box-shadow: 0 4px 6px rgba(0, 0, 0, 0.07);        /* card-hover */
box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1);       /* modal */
```

### Скругления
```python
BORDER_RADIUS = {
    'sm': '4px',   # inputs, buttons
    'md': '8px',   # cards
    'lg': '12px',  # panels
    'full': '9999px', # pills, badges
}
```

### Анимации (tooltips, hover)
```css
/* Базовый transition */
transition: all 0.2s ease;

/* Tooltip появление */
@keyframes fadeIn {
    from { opacity: 0; transform: translateY(-4px); }
    to { opacity: 1; transform: translateY(0); }
}

/* Hover эффект для графиков */
.chart-container:hover {
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.07);
    transform: translateY(-2px);
}
```

### Tooltips (обязательно для всех графиков)
```python
# Plotly hovertemplate
hovertemplate = (
    "<b>%{x}</b><br>"
    "Значение: %{y:,.0f}<br>"
    "<extra></extra>"  # убирает trace name
)
```

---

## Рекомендации по визуализации

> **Принцип:** Выбирай тип графика на основе данных и цели анализа. Ниже — рекомендации, не жесткие требования.

### Временные ряды
**Рекомендуется:** Line chart, Area chart
**Когда:** Показать изменение метрики во времени, тренды, сезонность

### Доли и пропорции
**Рекомендуется:** Stacked Bar, Treemap
**Избегать:** Pie/Donut charts
**Когда:** Показать части целого, вклад категорий

### Сравнение категорий
**Рекомендуется:** Bar chart (horizontal/vertical), Dot plot
**Когда:** Сравнить значения между группами

### Распределения
**Рекомендуется:** Histogram, Box plot, Violin plot
**Когда:** Понять распределение данных, выбросы, медианы

### Корреляции и связи
**Рекомендуется:** Scatter plot, Heatmap
**Когда:** Найти взаимосвязи между переменными

### Табличные данные
**Рекомендуется:** Styled DataFrame, DataTable с сортировкой
**Когда:** Нужна детализация, точные значения

---

## Layout структура

### Responsive Grid
**Система:** 12 columns (Streamlit `st.columns`)

```python
# Типичный layout
col1, col2, col3 = st.columns([1, 1, 1])  # 3 равные колонки
col1, col2 = st.columns([2, 1])           # 2/3 и 1/3
```

### Секции дашборда
```
┌─────────────────────────────────────────┐
│ Header: Заголовок + фильтры            │
├─────────────────────────────────────────┤
│ Metrics Row: KPI карточки (3-4 шт)     │
├─────────────────────────────────────────┤
│ Main Chart: Основной график (full)     │
├──────────────────┬──────────────────────┤
│ Chart 1 (50%)    │ Chart 2 (50%)       │
├──────────────────┴──────────────────────┤
│ Table: Детальные данные                │
└─────────────────────────────────────────┘
```

### Карточки метрик
```python
# Структура metric card
st.metric(
    label="Метрика",
    value="1,234",
    delta="12%",  # positive/negative автоматически
    delta_color="normal"  # "normal", "inverse", "off"
)
```

---

## Plotly базовый layout

```python
def get_base_layout(title: str, height: int = 400) -> dict:
    """Базовый layout для всех Plotly графиков."""
    return {
        'title': {
            'text': title,
            'font': {'size': 20, 'weight': 600, 'family': TYPOGRAPHY['font_family']},
            'x': 0,  # выравнивание слева
        },
        'font': {'family': TYPOGRAPHY['font_family'], 'size': 14},
        'plot_bgcolor': BRAND_COLORS['surface'],
        'paper_bgcolor': BRAND_COLORS['surface'],
        'height': height,
        'margin': {'l': 40, 'r': 20, 't': 60, 'b': 40},
        'hovermode': 'closest',
        'hoverlabel': {
            'bgcolor': 'white',
            'font_size': 13,
            'font_family': TYPOGRAPHY['font_family'],
        },
    }
```

---

## Пороги и статусы (Thresholds)

### Цветовая индикация метрик
```python
def get_metric_color(value: float, thresholds: dict) -> str:
    """
    Возвращает цвет на основе порогов.
    
    thresholds = {
        'target': 100,    # целевое значение
        'warning': 80,    # предупреждение
        'critical': 50,   # критично
        'direction': 'higher_is_better'  # или 'lower_is_better'
    }
    """
    direction = thresholds.get('direction', 'higher_is_better')
    
    if direction == 'higher_is_better':
        if value >= thresholds['target']:
            return BRAND_COLORS['success']
        elif value >= thresholds['warning']:
            return BRAND_COLORS['warning']
        else:
            return BRAND_COLORS['danger']
    else:  # lower_is_better
        if value <= thresholds['target']:
            return BRAND_COLORS['success']
        elif value <= thresholds['warning']:
            return BRAND_COLORS['warning']
        else:
            return BRAND_COLORS['danger']
```

---

## Accessibility (A11Y)

1. **Контраст:** Все цвета соответствуют WCAG AA (4.5:1 для текста)
2. **Alt-текст:** Для всех изображений и графиков
3. **Keyboard navigation:** Все элементы доступны с клавиатуры
4. **ARIA labels:** Для интерактивных элементов
5. **Font size:** Минимум 14px для основного текста

---

## Правила использования

### ✅ Правильно

```python
from dashboard_config import BRAND_COLORS, CHART_PALETTE_10, get_base_layout

fig = go.Figure(data=[go.Bar(
    marker={'color': BRAND_COLORS['primary']}
)])
fig.update_layout(get_base_layout('Заголовок'))
```

### ❌ Неправильно

```python
# Hardcoded цвета
fig = go.Figure(data=[go.Bar(marker={'color': '#8B5CF6'})])

# Неконсистентные размеры
st.markdown("### Заголовок", unsafe_allow_html=True)  # вместо st.header()
```

---

## Ключевые принципы

При создании дашборда помни:

- **Цвета:** Использовать палитру из `dashboard_config.py` (эко/здоровье тема, избегать фиолетового)
- **Компактность:** Spacing sm/md (8px/12px), не перегружать пространство
- **Интерактивность:** Tooltips на графиках, hover effects где уместно
- **Читаемость:** Шрифт Inter, числа с разделителями тысяч
- **Гибкость:** Тип графика выбирай исходя из данных и цели, используй рекомендации как ориентир

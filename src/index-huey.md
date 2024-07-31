# hello world

<script>
function resourceLoaded(element){
  var url = element.href || element.src;
  console.log(`Loaded ${url}`);
  var list = document.getElementById('resources');
  if (!list) {
    return;
  }
  var item = document.createElement('li');
  item.setAttribute('data-element', element.tagName);
  item.setAttribute('data-resource-type', url.split('?')[0].split('.').pop());
  item.innerText = url;
  list.appendChild(item);
}
</script><!-- Inline tabler font to force early load -->
<!-- see: https://cdn.jsdelivr.net/npm/@tabler/icons@3.10.0/ -->
<style type="text/css">
  @font-face {
    font-family: "tabler-icons";
    font-style: normal;
    font-weight: 400;
    font-display: block;
    src: url("https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@3.10.0/dist/fonts/tabler-icons.woff2?v3.10.0") format("woff2");
  }  ul#resources > li::marker {
    font-family: "tabler-icons";
    /* file */
    content: '\eaa4';
  }  ul#resources > li[data-resource-type=css]::marker {
    /* file-type-css */
    content: '\fb08';
  }
  ul#resources > li[data-resource-type=js]::marker {
    /* file-type-js */
    content: '\fb0e';
  }
  ul#resources > li[data-resource-type=woff2]::marker {
    /* file-typography */
    content: '\f041';
  }
</style><link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="Theme/General.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="spinner/spinner.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="spinner/timer.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="Tabs/Tabs.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="App/App.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="AboutDialog/AboutDialog.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="ErrorDialog/ErrorDialog.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="SettingsDialog/SettingsDialog.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="SettingsDialog/SettingsDialogLogic.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="ExportUi/ExportUi.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="UploadUi/UploadUi.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="Tree/Tree.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="DataSource/DataSourcesUi.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="util/resize/resize.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="Search/Search.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="AttributeUi/AttributeUi.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="QueryUi/QueryUi.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="FilterUi/FilterUi.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="PivotTableUi/PivotTableUi.css"/>
<link onload="resourceLoaded(this)" rel="stylesheet" type="text/css" href="PromptUi/PromptUi.css"/><div id="spinner">
  <div class="loader">Loading...</div>
  <ul id="resources" style="position:absolute; top: 0px" ></ul>
</div><dialog
  id="uploadUi"
  aria-labelledby="uploadUiTitle"
  aria-describedby="uploadUiDescription"
>
  <header>
    <h3 id="uploadUiTitle"></h3>
    <p id="uploadUiDescription">;</p>
    <div class="timer">
      <span class="digit"></span>
      <span class="digit"></span>
      <span class="digit"></span>
      <span class="digit"></span>
    </div>
  </header>
  <section id="uploadProgressList">  </section>
  <footer role="toolbar">
    <button
      id="uploadDialogOkButton"
    >Ok</button>
    <button
      id="uploadDialogCancelButton"
    >Cancel</button>
  </footer>
</dialog><dialog
  id="exportDialog"
  popover="manual"
  aria-labelledby="uploadUiTitle"
  aria-busy="false"
>
  <dialog role="progressbar">
    <header>
      <h3 role="status"></h3>
    </header>
    <section>
      <div class="loader loader-medium">Exporting...</div>
      <div class="timer">
        <span class="digit"></span>
        <span class="digit"></span>
        <span class="digit"></span>
        <span class="digit"></span>
      </div>
    </section>
    <footer>
      <!-- TODO: implement cancel of pending export -->
      <button id="cancelExportButton">Cancel</button>
    </footer>
  </dialog>
  <header>
    <h3 id="exportDialogTitle">Export...</h3>
    <form id="exportGeneralSettings">
      <label
        for="exportTitleTemplate"
        title="The title template is used to generate a file name for downloads"
      >Title template</label>
      <input
        id="exportTitleTemplate"
        title="The title template is used to generate a file name for downloads"
        value="${cells-items} from ${datasource} with ${rows-items} on rows and ${columns-items} on columns"
      />
      <label
        for="exportTitle"
        title="The title generated from the template"
      >Title</label>
      <output
        id="exportTitle"
        for="exportTitleTemplate"
        title="The title generated from the template"
      ></output>
      <fieldset>
        <legend title="Control the shape of the exported dataset">Data Structure</legend>
        <label
          for="exportResultShapePivot"
          title="Export results as a pivot table"
        >Pivot</label>
        <input
          id="exportResultShapePivot"
          type="radio"
          name="exportResultShape"
          checked="true"
          title="Check this to export results as a pivot table"
        />
        <label
          for="exportResultShapeTable"
          title="Export results as a plain table. In this format, all items from the query are used to produce a list of rows "
        >Table</label>
        <input
          id="exportResultShapeTable"
          type="radio"
          name="exportResultShape"
          title="Check this to export results as a plain table"
        />
      </fieldset>
      <fieldset>
        <legend title="Control where the results are exported to">Export destination</legend>
        <label
          for="exportDestinationFile"
          title="Download the export data as a file so you can store it on your system."
        >File</label>
        <input
          id="exportDestinationFile"
          type="radio"
          name="exportDestination"
          checked="true"
          title="Check this to download the result as a file"
        />
        <label
          for="exportDestinationClipboard"
          title="Copy the export data to the clipboard"
        >Clipboard</label>
        <input
          id="exportDestinationClipboard"
          type="radio"
          name="exportDestination"
          title="Check this to copy the export data to the clipboard so you can paste it in other applications"
        />
      </fieldset>
    </form>
  </header>
  <section role="tablist">
    <!--
      See: https://duckdb.org/docs/sql/statements/copy.html#csv-options
    -->
    <div>
      <label
        role="tab"
        for="exportDelimited"
        title="Use this tab to export data as delimited text, like .CSV, TSV, etc."
      >Delimited text</label>
      <input id="exportDelimited" name="exportFormat" type="radio" checked="true"/>
      <div role="tabpanel">
        <form id="exportDelimitedSettings">
          <label
            for="exportDelimitedCompression"
            title="The algorithm used for compressing the query result. Compression typically results in smaller result files."
          >Compression</label>
          <select
            id="exportDelimitedCompression"
            title="Use this to choose the algorithm used for compressing the query result."
          >
            <option
              selected="true"
              title="Uncompressed - no compression will be applied"
              value="UNCOMPRESSED"
            >uncompressed</option>
            <option
              title="GZIP - applies gzip compression"
              value="GZIP"
            >gzip</option>
            <option
              title="ZTSD - applies ztsd compression"
              value="ZTSD"
            >ztsd</option>
          </select>
          <label
            title="Whether to include a line of column headers."
            for="exportDelimitedIncludeHeaders"
          >Include Headers</label>
          <input
            id="exportDelimitedIncludeHeaders"
            title="Check this to include a header line of column names."
            type="checkbox"
            checked="true"
          />
          <fieldset>
            <legend>Formatting</legend>
            <label
              for="exportDelimitedDateFormat"
              title="The date format controls how date values are represented in the result."
            >Date Format</label>
            <input
              id="exportDelimitedDateFormat"
              title="Enter a valid DuckDB date format string."
              type="text"
              value="%x"
            />
            <label
              for="exportDelimitedTimestampFormat"
              title="The timestamp format controls how timestamp values are represented in the result."
            >Timestamp Format</label>
            <input
              id="exportDelimitedTimestampFormat"
              title="Enter a valid DuckDB timestamp format string."
              type="text"
              value="%c"
            />
            <label
              for="exportDelimitedNullString"
              title="The NULL-string controls how SQL NULL-values are rendered to the result"
            >NULL-value string</label>
            <input
              id="exportDelimitedNullString"
              title="Enter the string that should be written to the result to represent SQL NULL-values"
              type="text"
              value=""
            />
          </fieldset>
          <fieldset>
            <legend>Delimiters</legend>
            <label
              for="exportDelimitedColumnDelimiter"
              title="The column delimiter is the character used to separate the values within a row in the result."
            >Column delimiter</label>
            <input
              id="exportDelimitedColumnDelimiter"
              type="text"
              value=","
              title="Enter the character that is to be used as column delimiter."
            />
            <label
              for="exportDelimitedQuote"
              title="The quote character is used to enclose column values in case the column value contains a delimiter character"
            >Quote Character</label>
            <input
              id="exportDelimitedQuote"
              type="text"
              value="&quot;"
              title="Enter the character that is to be used as quote character."
            />
            <label
              for="exportDelimitedEscape"
              title="The escape character is used to signal a literal occurrence of the quote character within a column value"
            >Escape Character</label>
            <input
              id="exportDelimitedEscape"
              type="text"
              value="&quot;"
              title="Enter the character used to escape the quote character."
            />
          </fieldset>
        </form>
      </div>
    </div>
    <!--
      See: https://duckdb.org/docs/sql/statements/copy.html#json-options
    -->
    <div>
      <label
        role="tab"
        for="exportJson"
        title="Use this tab to export data in the JSON format"
      >JSON</label>
      <input id="exportJson" name="exportFormat" type="radio"/>
      <div role="tabpanel">
        <form id="exportJsonSettings">
          <label
            for="exportJsonCompression"
            title="Use this to choose the algorithm used for compressing the query result."
          >Compression</label>
          <select
            id="exportJsonCompression"
            title="Use this to choose the algorithm used for compressing the query result."
          ></select>
          <fieldset>
            <legend>Formatting</legend>
            <label
              for="exportJsonDateFormat"
              title="The date format controls how date values are represented in the result."
            >Date Format</label>
            <input
              id="exportJsonDateFormat"
              type="text"
              value="%x"
              title="Enter a valid DuckDB date format string."
            />
            <label
              for="exportJsonTimestampFormat"
              title="The timestamp format controls how timestamp values are represented in the result."
            >Timestamp Format</label>
            <input
              id="exportJsonTimestampFormat"
              type="text"
              title="Enter a valid DuckDB timestamp format string."
              value="%c"
            />
          </fieldset>
          <fieldset>
            <legend>Delimiters</legend>
            <label
              for="exportJsonRowDelimiter"
              title="This controls how rows are delimited in the JSON output"
            >Row delimiter</label>
            <select
              id="exportJsonRowDelimiter"
              title="This controls how rows are delimited in the JSON output"
            ></select>
          </fieldset>
        </form>
      </div>
    </div>
    <!--
      See: https://duckdb.org/docs/sql/statements/copy.html#parquet-options
    -->
    <div>
      <label
        role="tab"
        for="exportParquet"
        title="Use this tab to export data in Parquet format"
      >Parquet</label>
      <input id="exportParquet" name="exportFormat" type="radio"/>
      <div role="tabpanel">
        <form id="exportParquetSettings">
          <label
            for="exportParquetCompression"
            title="Use this to choose the algorithm used for compressing the query result."
          >Compression</label>
          <select
            id="exportParquetCompression"
            title="Use this to choose the algorithm used for compressing the query result."
          ></select>
        </form>
      </div>
    </div>
    <div>
      <label
        role="tab"
        for="exportSql"
        title="Use this tab to export a SQL query that would produce this result."
      >SQL</label>
      <input id="exportSql" name="exportFormat" type="radio"/>
      <div role="tabpanel">
        <form id="exportSqlSettings">
          <label
            for="exportSqlKeywordLettercase"
            title="The lettercase for SQL keywords"
          >Keywords Case</label>
          <select
            title="The lettercase for SQL keywords"
            id="exportSqlKeywordLettercase"
          >
            <option
              title="Initial capital followed by lowercase"
              value="initialCapital">Initial Capital</option>
            <option
              title="Lowercase"
              value="lowerCase">Lower Case</option>
            <option
              title="Uppercase"
              value="upperCase"
              selected="true">Upper Case</option>
          </select>
          <label
            for="exportSqlAlwaysQuoteIdentifiers"
            title="Whether to always quote identifiers."
          >Always Quote identifiers</label>
          <input
            id="exportSqlAlwaysQuoteIdentifiers"
            title="Check this to force all identifiers to be quoted."
            checked="true"
            type="checkbox"
          />
          <label
            for="exportSqlCommaStyle"
            title="How to render commas in the SQL output"
          >Comma style</label>
          <select
            title="Select the style for rendering commas in the SQL output"
            id="exportSqlCommaStyle"
          >
            <option
              value="spaceAfter">Space After</option>
            <option
              value="newlineAfter">Newline After</option>
            <option
              value="newlineBefore"
              selected="true">Newline Before</option>
          </select>
        </form>
      </div>
    </div>
  </section>
  <footer role="toolbar">
    <button
      id="exportDialogCloseButton"
      popovertarget="exportDialog"
      popovertargetaction="hide"
    >Close</button>
    <button
      id="exportDialogExecuteButton"
    >Export</button>
  </footer>
</dialog><dialog
  id="filterDialog"
  aria-busy="false"
  popover="auto"
>
  <header role="toolbar">
    <label 
      for="filterType" 
      title="The filter type determines how the selected values will be used to filter the results."
    >Filter type:</label>
    <select id="filterType">
      <option value="in" title="Include data that matches any of the selected values">Include</option>
      <option value="notin" title="Exclude data that matches any of the selected values">Exclude</option>
      <option value="between" title="Include data within any of the specified value ranges">Between</option>
      <option value="notbetween" title="Exclude data within any of the specified value ranges">Not Between</option>
    </select>
  </header>
  <section>
    <header>
      <menu role="toolbar">
        <label
          for="filterSearchApplyAll"
          title="Check to include the other filter items (in addition to the search string) to populate the picklist"
        >
          Apply all filters:
          <input id="filterSearchApplyAll" type="checkbox"/>
        </label>
      </menu>
      <section>
        <div id="filterDialogSpinner" class="loader loader-medium"></div>
        <header>
          <input
            id="filterSearch"
            placeholder="Use a LIKE pattern to find values..."
            type="search"
            title="Enter a search string to filter the value picklist (LIKE wildcards supported)"
          />
        </header>
        <section>
          <select
            id="filterPicklist"
            multiple="true"
            size="5"
            title="Choose values from the picklist to add them to the Filter values list. Hold SHIFT-key to select multiple items."
          >
          </select>
        </section>
        <footer id="filterSearchStatus" role="status">No values found.</footer>
      </section>
    </header>
    <section>
      <div>
        <label for="filterValueList">Select values:</label>
        <select
          id="filterValueList"
          multiple="true"
          size="7"
          title="Values in this list will be used to filter the results. Add items to the list by choosing from the picklist above; click items in the list to remove them."
        >
        </select>
      </div>
      <div>
        <label for="toFilterValueList">To Values:</label>
        <select
          id="toFilterValueList"
          multiple="true"
          size="7"
          title="Values in this list will be used to filter the results. Add items to the list by choosing from the picklist above; click items in the list to remove them."
        >
        </select>
      </div>
    </section>
    <footer id="filterValueSelectionStatus" role="status"></footer>
    <footer role="toolbar">
      <button id="filterDialogClearSelectedButton" title="Clear highlighted items from the selection.)">Clear Highlighted</button>
      <button id="filterDialogClearButton" title="Clear the values list">Clear All</button>
    </footer>
  </section>
  <footer role="toolbar">
    <button
      id="filterDialogOkButton"
      title="Confirm the filter setting changes"
      popovertarget="filterDialog"
      popovertargetaction="hide"
    >Apply</button>
    <button
      id="filterDialogRemoveButton"
      title="Remove the filter from the axis"
      popovertarget="filterDialog"
      popovertargetaction="hide"
    >Remove</button>
    <button
      id="filterDialogCancelButton"
      title="Cancel filter setting changes"
      popovertarget="filterDialog"
      popovertargetaction="hide"
    >Cancel</button>
  </footer>
</dialog><dialog
  id="errorDialog"
  popover="auto"
  aria-labelledby="errorDialogTitle"
  aria-describedby="errorDialogDescription"
>
  <header>
    <h3 id="errorDialogTitle"></h3>
  </header>
  <section id="errorDialogDescription">
  </section>
  <footer role="toolbar">
    <button
      id="errorDialogOkButton"
      popovertarget="errorDialog"
      popovertargetaction="hide"
    >Ok</button>
  </footer>
</dialog><dialog
  id="settingsDialog"
  aria-labelledby="settingsDialogTitle"
  popover="manual"
>
  <header>
    <h3 id="settingsDialogTitle">Settings</h3>
  </header>
  <section
    id="settingsTabs"
    role="tablist"
  >
    <!--
      Datasources settings
    -->
    <div>
      <label
        role="tab"
        for="datasourcesSettingTab"
      >
        Datasources
      </label>
      <input id="datasourcesSettingTab" type="radio" name="settingsTabs" checked="true"/>
      <div role="tabpanel">
        <form id="datasourceSettings">
          <label 
            for="useLooseColumnTypeComparison" 
            title="Whether to use exact or loose typing for automatic creation of UNION datasources."
          >UNION loose typing</label>
          <input id="useLooseColumnTypeComparison" type="checkbox"/>
        </form>
      </div>
    </div>
    <!--
      Locale Settings
    -->
    <div>
      <label
        role="tab"
        for="localeSettingsTab"
      >
        Value Formatting
      </label>
      <input id="localeSettingsTab" type="radio" name="settingsTabs"/>
      <div role="tabpanel">
        <form id="localeSettings">
          <label 
            for="nullString"
            title="The string to use for displaying NULL-values"
          >NULL-value label</label>
          <input id="nullString" type="input"/>
          <label 
            for="totalsString"
            title="The string to use for displaying totals"
          >Totals label</label>
          <input id="totalsString" type="input"/>
          <label 
            for="useDefaultLocale"
            title="Check to use the browser's default locale, uncheck to enter a custom locale."
          >Use default locale</label>
          <input id="useDefaultLocale" type="checkbox"/>
          <!--
            see: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl
            A locale identifier is a string that consists of:            A language subtag with 2–3 or 5–8 letters
            A script subtag with 4 letters Optional
            A region subtag with either 2 letters or 3 digits Optional
            One or more variant subtags (all of which must be unique), each with either 5–8 alphanumerals or a digit followed by 3 alphanumerals Optional
            One or more BCP 47 extension sequences Optional
            A private-use extension sequence Optional
          -->
          <label 
            for="locale"
            title="The locale to use for creating value formatters"
          >Locale</label>
          <!--
            on change we should try to call Intl.DisplayNames.supportedLocalesOf('DE-AU'). this will return an array
            and if that is empty it probably means the entered locale is either not valid or not supported.
          -->
          <input id="locale"
            pattern="^(([A-Za-z]{2,3}|[A-Za-z]{5,8})(-[A-Za-z]{4})?(-([A-Za-z]{2}|\d{3}))?(-([0-9A-Za-z]{5,8}|\d[0-9A-Za-z]{3}))?)(\s*,\s*(([A-Za-z]{2,3}|[A-Za-z]{5,8})(-[A-Za-z]{4})?(-([A-Za-z]{2}|\d{3}))?(-([0-9A-Za-z]{5,8}|\d[0-9A-Za-z]{3}))?))*$"
            data-value-getter="new Function('control','settings','return control.value.split(String.fromCharCode(44));')"
            data-value-setter="new Function('control','value','settings','control.value = value.join();')"
          />
          <!-- minimum integer digits -->
          <label for="minimumIntegerDigits"
            title="The minimum number of integer digits to use. A value with a smaller number of integer digits than this number will be left-padded with zeros (to the specified length) when formatted. Possible values are from 1 to 21; the default is 1."
          >Min. integer digits</label>
          <input id="minimumIntegerDigits" type="number" min="1" max="21" value="1"/>
          <!-- minimum fraction digits -->
          <label for="minimumFractionDigits"
            title="The minimum number of fraction digits to use. .Possible values are from 0 to 20; the default for plain number and percent formatting is 0; the default for currency formatting is the number of minor unit digits provided by the ISO 4217 currency code list (2 if the list doesn't provide that information)."
          >Min. fraction digits</label>
          <input id="minimumFractionDigits" type="number" min="0" max="20" value="2"/>
          <!-- maximum fraction digits -->
          <label for="maximumFractionDigits"
            title="The maximum number of fraction digits to use. Possible values are from 0 to 20; the default for plain number formatting is the larger of minimumFractionDigits and 3; the default for currency formatting is the larger of minimumFractionDigits and the number of minor unit digits provided by the ISO 4217 currency code list (2 if the list doesn't provide that information); the default for percent formatting is the larger of minimumFractionDigits and 0."
          >Max. fraction digits</label>
          <input id="maximumFractionDigits" type="number" min="0" max="20" value="2"/>
        </form>
      </div>
    </div>    <!--
      Query settings
    -->
    <div>
      <label
        role="tab"
        for="querySettingsTab"
      >
        Query
      </label>
      <input id="querySettingsTab" type="radio" name="settingsTabs"/>
      <div role="tabpanel">
        <form id="querySettings">
          <label 
            for="autoRunQuery"
            title="When enabled the pivot table is updated automatically after modifying the query. When disabled, you have to explicitly hit the execute button."
          >Autorun Query</label>
          <input id="autoRunQuery" type="checkbox"/>
        </form>
      </div>
    </div>    <!--
      Pivot Table
    -->
    <div>
      <label
        role="tab"
        for="pivotSettingsTab"
      >
        Pivot Table
      </label>
      <input id="pivotSettingsTab" type="radio" name="settingsTabs"/>
      <div role="tabpanel">
        <form id="pivotSettings">
          <label for="maxCellWidth"
            title="The maximum string length to consider when sizing pivot table cells and headers"
          >Max cellwidth (ch)</label>
          <input id="maxCellWidth" type="number" min="1" max="256" value="30"/>
        </form>
      </div>
    </div>    <!--
      Theme
    -->
    <div>
      <label
        role="tab"
        for="themeSettingsTab"
      >
        Theme
      </label>
      <input id="themeSettingsTab" type="radio" name="settingsTabs"/>
      <div role="tabpanel">
        <form id="themeSettings">
          <label for="themes">Themes</label>
          <select
            id="themes"
            onchange="Theme.applyTheme(this.selectedIndex)"
            data-value-getter="new Function('control', 'settings', 'return JSON.parse(control.value);')"
            data-value-setter="new Function('control', 'value', 'settings', 'control.value = JSON.stringify(value);')"
          >
          </select>
        </form>
      </div>
    </div>
  </section>
  <footer role="toolbar">
    <button
      id="settingsDialogOkButton"
      popovertarget="settingsDialog"
      popovertargetaction="hide"
    >Ok</button>
    <button
      id="settingsDialogResetButton"
    >Reset All</button>
    <button
      id="settingsDialogCancelButton"
      popovertarget="settingsDialog"
      popovertargetaction="hide"
    >Cancel</button>
  </footer>
</dialog><dialog
  id="promptUi"
  aria-labelledby="promptDialogTitle"
  popover="manual"
>
  <header>
    <h3 id="promptDialogTitle"></h3>
  </header>
  <section>
  </section>
  <footer role="toolbar">
    <form id="promptUiForm" method="dialog">
    </form>
    <button
      id="promptDialogAcceptButton"
      form="promptUiForm"
      popovertarget="promptUi"
      popovertargetaction="hide"
    >Yes</button>
    <button
      id="promptDialogRejectButton"
      form="promptUiForm"
      popovertarget="promptUi"
      popovertargetaction="hide"
    >No</button>
  </footer>
</dialog><dialog
  id="aboutDialog"
  aria-labelledby="aboutDialogTitle"
  popover="auto"
>
  <header>
    <h3 id="aboutDialogTitle">About Huey...</h3>
  </header>
  <section>
    <p>
      A DuckDB User Interface
    </p>
    <ul>
      <li>Huey version 0.0.5 - Shelduck</li>
      <li><a href="https://duckdb.org/" target="_duckdb" id="duckdbVersionLabel"></a></li>
      <li><a href="https://cdn.jsdelivr.net/npm/@duckdb/duckdb-wasm@1.28.1-dev242.0/+esm" target="jsdelivr">DuckDB WASM 1.28.1-dev242.0</a></li>
      <li><a href="https://tabler.io/icons" target="_tabler-icons">Tabler Icons v3.10.0</a></li>
      <li><a href="https://github.com/rpbouman/huey/" target="_github">Huey Source on Github</a></li>
      <li><a href="https://raw.githubusercontent.com/rpbouman/huey/dev/LICENSE" target="_github">License (MIT)</a></li>
    </ul>
    <p style="font-size: smaller">Created and maintained by Roland.Bouman@gmail.com</p>
    <p><a href="https://www.paypal.com/donate/?hosted_button_id=776A6UNZ35M84" target="_donate">Donations help to keep Huey in good shape!</a></p>
  </section>
  <footer role="toolbar">
    <button
      id="aboutDialogOkButton"
      popovertarget="aboutDialog"
      popovertargetaction="hide"
    >Ok</button>
    <button
      title="Donate and help to keep Huey developed and maintained"
      onclick="window.open('https://www.paypal.com/donate/?hosted_button_id=776A6UNZ35M84', '_donate')"
      style="width: 7em"
    >Donate...</button>
  </footer>
</dialog><dialog 
  id="datasourceSettingsDialog"
  aria-labelledby="datasourceSettingsDialogTitle"
  popover="auto"
>
  <header>
    <h3 id="datasourceSettingsDialogTitle">Datasource Settings</h3>
    <form>
      <label for="datasourceFileType">Type</label>
      <output id="datasourceFileType"></output>
      <label for="datasourceName">Type</label>
      <output id="datasourceName"></output>
    </form>
  </header>
  <section>
  </section>
  <footer role="toolbar">
    <button
      id="datasourceSettingsDialogOkButton"
      popovertarget="datasourceSettingsDialog"
      popovertargetaction="hide"
    >Ok</button>
    <button
      id="datasourceSettingsDialogCancelButton"
      popovertarget="datasourceSettingsDialog"
      popovertargetaction="hide"
    >Cancel</button>
  </footer>
</dialog><main
  id="layout"
  class="layout"
  style="display: none"
>
  <menu class="toolbar" role="toolbar">
    <label for="uploader" title="Register local data files to explore their contents with Huey">
      <input
        id="uploader"
        type="file"
        multiple="true"
        accept=".csv,.duckdb,.json,.parquet,.sql,.sqlite,.tsv,.xlsx"
      />
    </label>    <label for="runQueryButton" title="Execute Query">
      <button
        id="runQueryButton"
      >Execute Query</button>
    </label>    <label for="autoRunQuery" title="Check this if you want to execute the query automatically">Autorun Query</label>    <!-- title in the toolbar identifies the currently selected datasource -->
    <h1 id="currentDatasource"></h1>    <label
      for="aboutButton"
      class="aboutButton"
      title="About Huey..."
    >
      <button
        id="aboutButton"
        popovertarget="aboutDialog"
        popovertargetaction="show"
      >About</button>
    </label>    <label
      for="settingsButton"
      class="button settings"
      title="Open the Huey Settings dialog."
    >
      <button
        id="settingsButton"
        popovertarget="settingsDialog"
        popovertargetaction="show"
      >Settings</button>
    </label>    <label
      for="exportButton"
      class="button"
      title="Export &amp; Download queries and/or result data..."
      style="visibility: hidden"
    >
      <button
        id="exportButton"
        popovertarget="exportDialog"
        popovertargetaction="show"
      >Download</button>
    </label>
  </menu>
  <nav
    role="tablist"
    id="sidebar"
    class="resizeHorizontal"
  >
    <!-- Datasources tab -->
    <div    >
      <label
        for="datasourcesTab"
        role="tab"
        title="Files, database tables and so on that provide data you'd like to explore."
      >Datasources</label>
      <input id="datasourcesTab" type="radio" name="sidebarTabs" checked="true"/>
      <div
        role="tabpanel"
      >
        <div
          id="datasourcesUi"
          role="tree"
        ></div>
      </div>
    </div>    <!-- Attributes tab -->
    <div>
      <label
        for="attributesTab"
        role="tab"
        title="Columns, formulas and aggregates to query and pivot"
      >Attributes</label>
      <input id="attributesTab" type="radio" name="sidebarTabs"/>
      <div role="tabpanel">
        <search
          id="searchAttributeUi"
          class="search"
          style="display:none"
        >
          <fieldset>
            <legend id="searchAttributesLabel">Search Attributes</legend>
            <input
              id="searchAttribute"
              type="search"
              placeholder="Search by Attribute name"
              title="Enter a search term to find matching attributes"
              aria-labelledby="searchAttributesLabel"
            />
          </fieldset>
        </search>
        <div
          id="attributeUi"
          class="attributeUi"
          style="flex-grow: 1;"
          role="tree"
        >
        </div>
      </div>
    </div>  </nav>
  <div class="workarea">
    <div
      id="queryUi"
      class="queryUi"
      data-cellheadersaxis="columns"
      style="display: none"
    >
      <template id="queryUiAxis">
        <section>
          <header>
            <label><button id="-axis-primary-action"></button></label>
            <h1>Axis Caption</h1>
          </header>
          <ol>
          </ol>
          <footer>
            <label title="Clear all items from this axis"><button id="-clear-axis">Clear axis</button></label>
          </footer>
        </section>
      </template>      <template id="queryUiAxisItem">
        <li>
          <label title="Move this item to the left"><button id="-move-left">Move item left</button></label>
          <span>caption</span>
          <menu>
            <label title="Calculate totals for this level"><input id="-toggle-totals" type="checkbox"/></label>
            <label title="Move this item to the other axis"><button id="-move-to-other-axis">Move item to other axis</button></label>
            <label title="Remove this item from the axis"><button id="-remove-from-axis">Remove item from axis</button></label>
          </menu>
          <label title="Move this item to the right"><button id="-move-right">Move item right</button></labe>
        </li>
      </template>      <template id="queryUiFilterAxisItem">
        <li>
          <label title="Move this item to the left"><button id="-move-left">Move item left</button></label>
          <details>
            <summary>
              <span>caption</span>
            </summary>
            <ol></ol>
          </details>
          <menu>
            <label title="Click to open the filter dialog to edit the filter."><button id="-edit-filter-condition">Click to open the filter dialog to edit the filter.</button></label>
            <label title="Remove this item from the axis"><button id="-remove-from-axis">Remove item from axis</button></label>
          </menu>
          <label title="Move this item to the right"><button id="-move-right">Move item right</button></labe>
        </li>
      </template>
    </div>
    <!-- pivotTableUi: outmost container of the pivot table-->
    <div
      id="pivotTableUi"
      class="pivotTableUiContainer"
      style="
        flex-grow: 1;
        width: 100%;
        height: 100%;
        border-width: 1px;
        border-color: var( --huey-dark-border-color );
        border-top-style: solid;
      "
      aria-busy="false"
      data-needs-update="false"
    >
      <dialog role="progressbar">
        <header>
          <div class="loader loader-medium">Loading...</div>
          <div class="timer">
            <span class="digit"></span>
            <span class="digit"></span>
            <span class="digit"></span>
            <span class="digit"></span>
          </div>
        </header>
        <section>
          <!-- TODO: actual progress information -->
        </section>
        <footer>
          <button id="cancelQueryButton">Cancel</button>
        </footer>
      </dialog>
      <div
        class="pivotTableUiInnerContainer"
      >
        <!-- pivotTableColumnsSizer: sizer to generate the horizontal scrollbar -->
        <div class="pivotTableUiSizer pivotTableUiHorizontalSizer"></div>
        <!-- pivotTableColumnsSizer: sizer to generate the vertical scrollbar -->
        <div class="pivotTableUiSizer pivotTableUiVerticalSizer"></div>        <!-- the actual table structure -->
        <div
          class="pivotTableUiTable"
        >
          <div class="pivotTableUiTableHeader"></div>
          <div class="pivotTableUiTableBody"></div>
        </div>
      </div>
    </div>
  </div>
</main><script onload="resourceLoaded(this)" src="util/dom/dom.js"></script>
<script onload="resourceLoaded(this)" src="util/clipboard/clipboard.js"></script>
<script onload="resourceLoaded(this)" src="util/event/EventEmitter.js"></script>
<script onload="resourceLoaded(this)" src="util/event/EventBuffer.js"></script>
<script onload="resourceLoaded(this)" src="Tabs/Tabs.js"></script><script onload="resourceLoaded(this)" src="SettingsDialog/SettingsDialog.js"></script>
<script onload="resourceLoaded(this)" src="Theme/Theme.js"></script><script onload="resourceLoaded(this)" src="util/sql/SQLHelper.js"></script>
<script onload="resourceLoaded(this)" src="DataSource/duckdb/DuckDbConnection.js"></script>
<script onload="resourceLoaded(this)" src="DataSource/duckdb/DuckDbDataSource.js"></script>
<script onload="resourceLoaded(this)" src="DataSet/DataSetComponent.js"></script>
<script onload="resourceLoaded(this)" src="DataSet/TupleSet.js"></script>
<script onload="resourceLoaded(this)" src="DataSet/CellSet.js"></script>
<script onload="resourceLoaded(this)" src="ErrorDialog/ErrorDialog.js"></script>
<script onload="resourceLoaded(this)" src="UploadUi/UploadUi.js"></script>
<script onload="resourceLoaded(this)" src="ExportUi/ExportUi.js"></script>
<script onload="resourceLoaded(this)" src="DataSource/DataSourcesUi.js"></script>
<script onload="resourceLoaded(this)" src="AttributeUi/AttributeUi.js"></script>
<script onload="resourceLoaded(this)" src="Search/Search.js"></script>
<script onload="resourceLoaded(this)" src="QueryModel/QueryModel.js"></script>
<script onload="resourceLoaded(this)" src="QueryUi/QueryUi.js"></script>
<script onload="resourceLoaded(this)" src="FilterUi/FilterUi.js"></script>
<script onload="resourceLoaded(this)" src="PivotTableUi/PivotTableUi.js"></script>
<script onload="resourceLoaded(this)" src="Routing/Routing.js"></script>
<script onload="resourceLoaded(this)" src="PromptUi/PromptUi.js"></script>
<script onload="resourceLoaded(this)" src="PageStateManager/PageStateManager.js"></script><script onload="resourceLoaded(this)" src="App/App.js"></script>
<script type="module">
  import * as duckdb from 'https://cdn.jsdelivr.net/npm/@duckdb/duckdb-wasm@1.28.1-dev242.0/+esm';  const JSDELIVR_BUNDLES = duckdb.getJsDelivrBundles();
  const bundle = await duckdb.selectBundle(JSDELIVR_BUNDLES);  const worker_url = URL.createObjectURL(
    new Blob([`importScripts("${bundle.mainWorker}");`], {type: 'text/javascript'})
  );
  const worker = new Worker(worker_url);
  const logger = new duckdb.ConsoleLogger();
  const db = new duckdb.AsyncDuckDB(logger, worker);
  URL.revokeObjectURL(worker_url);  await db.instantiate(bundle.mainModule, bundle.pthreadWorker);
  const connection = await db.connect();  window.hueyDb = {
    duckdb: duckdb,
    instance: db,
    connection: connection
  };  initApplication();</script>
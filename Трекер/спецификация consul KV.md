<macro class="toc op-uc-placeholder op-uc-toc">
</macro>

# Спецификация

## bootstorage

Раздел описывающий варианты загрузки

### device-&lt;arch&gt;

ARCH:

<figure class="table op-uc-figure_align-center op-uc-figure"><table class="op-uc-table" style="border-color:hsl(0, 0%, 0%);border-style:solid;"><thead class="op-uc-table--head"><tr class="op-uc-table--row"><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Значение</th></tr></thead><tbody><tr class="op-uc-table--row"><td class="op-uc-p op-uc-table--cell">x86_64</td></tr><tr class="op-uc-table--row"><td class="op-uc-p op-uc-table--cell">arm64</td></tr></tbody></table></figure>

Значение: JSON

<figure class="table op-uc-figure_align-center op-uc-figure"><table class="op-uc-table"><thead class="op-uc-table--head"><tr class="op-uc-table--row"><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Поле</th><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Обязательное</th><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Значение</th></tr></thead><tbody><tr class="op-uc-table--row"><td class="op-uc-p op-uc-table--cell">target_boot_type</td><td class="op-uc-p op-uc-table--cell">да</td><td class="op-uc-table--cell"><p class="op-uc-p">тип загрузки из:</p><ul class="op-uc-list"><li class="op-uc-list--item">netboot</li><li class="op-uc-list--item">install</li></ul></td></tr><tr class="op-uc-table--row"><td class="op-uc-p op-uc-table--cell">target_os</td><td class="op-uc-p op-uc-table--cell">да</td><td class="op-uc-table--cell"><p class="op-uc-p">Название ОС из (неполный список):</p><ul class="op-uc-list"><li class="op-uc-list--item">CentOS</li><li class="op-uc-list--item">Debian</li><li class="op-uc-list--item">Ubuntu</li></ul></td></tr><tr class="op-uc-table--row"><td class="op-uc-p op-uc-table--cell">target_image</td><td class="op-uc-p op-uc-table--cell">да</td><td class="op-uc-p op-uc-table--cell">Название образа</td></tr><tr class="op-uc-table--row"><td class="op-uc-p op-uc-table--cell">target_variant</td><td class="op-uc-p op-uc-table--cell">нет</td><td class="op-uc-p op-uc-table--cell">название варианта загрузки образа из boot.json</td></tr></tbody></table></figure>

### &lt;MAC&gt;

MAC:

MAC адрес в формате с двоеточиями, например `00:e0:ed:df:8f:41`

Значение:

такое  же как для device-&lt;arch&gt;

## global

содержит различные настройки, связанные со всей площадкой тестирования

### ansible.cfg

полная конфигурация ansible для тестирования, используется при запуске тестирования, появляется на узле по пути `/etc/ansible/testing_ansible.cfg`

### plugins\_commit\_hash

commit hash репозитория factorytesting/ansible/plugins который используется во время testprepare

### ask\_serial\_at\_boot

<figure class="table op-uc-figure_align-center op-uc-figure"><table class="op-uc-table"><tbody><tr class="op-uc-table--row"><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Type</th><td class="op-uc-p op-uc-table--cell">Bool</td></tr><tr class="op-uc-table--row"><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Назначение</th><td class="op-uc-p op-uc-table--cell">определяет будет ли загрузчик iPXE запрашивать серийный номер и пытаться автоматически вычислить образ загрузки для включающегося устройства</td></tr><tr class="op-uc-table--row"><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Обязательное</th><td class="op-uc-p op-uc-table--cell">нет</td></tr><tr class="op-uc-table--row"><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Значение при отсутствии</th><td class="op-uc-p op-uc-table--cell">False</td></tr></tbody></table></figure>

### ask\_user\_id

<figure class="table op-uc-figure_align-center op-uc-figure"><table class="op-uc-table"><tbody><tr class="op-uc-table--row"><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Type</th><td class="op-uc-p op-uc-table--cell">Bool</td></tr><tr class="op-uc-table--row"><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Назначение</th><td class="op-uc-p op-uc-table--cell">определяет используется ли на данном заводе идентификация операторов</td></tr><tr class="op-uc-table--row"><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Обязательное</th><td class="op-uc-p op-uc-table--cell">нет</td></tr><tr class="op-uc-table--row"><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Значение при отсутствии</th><td class="op-uc-p op-uc-table--cell">False</td></tr></tbody></table></figure>

### device\_fail\_reason

## device\_current\_stage

## testconfigs

Раздел, описывающий маппинги конфигураций, в котором каждый ключ один маппинг

### &lt;Device range&gt;

Device range: строка серийного номера с одним диапазоном, заключенным в квадратные скобки, например `AX300M[000001-999999]` Приведенный диапазон отвечает за серийные номера с `AX300M000001` по `AX300M999999`. Регистор букв значения не имеет

<figure class="table op-uc-figure_align-center op-uc-figure"><table class="op-uc-table"><tbody><tr class="op-uc-table--row"><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Type</th><td class="op-uc-table--cell"><p class="op-uc-p">str: &lt;repo name&gt;[:version]</p><p class="op-uc-p">repo name - название репозитория с конфигурацией по ссыке http://git.service&lt;robot fqdn&gt;/factorytesting/projects/&lt;repo name&gt;.git например <code class="op-uc-code">http://git.service.robot3.aq.ru/factorytesting/projects/aqx300m.git</code></p></td></tr><tr class="op-uc-table--row"><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Назначение</th><td class="op-uc-p op-uc-table--cell">определяет название гит репозитория и версию (если указана)</td></tr><tr class="op-uc-table--row"><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Обязательное</th><td class="op-uc-p op-uc-table--cell">да</td></tr><tr class="op-uc-table--row"><th class="op-uc-p op-uc-table--cell op-uc-table--cell_head">Значение при отсутствии</th><td class="op-uc-p op-uc-table--cell">N/A</td></tr></tbody></table></figure>
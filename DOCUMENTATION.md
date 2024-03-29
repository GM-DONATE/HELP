# Итемы
Итемы — основа этого скрипта. Каждый итем является отдельной донат услугой и имеет свой уникальный идентификатор (UID)

`IGS("Имя","unique_id")` — _добавляет услугу (итем) под названием "**Имя**" и с УНИКАЛЬНЫМ id "**unique_id**"_. К этому итему применяются методы, которые описаны ниже

## Основные методы
|Метод|Описание|
|---|---|
|:SetDescription("**Блабла**")| Устанавливает текст, который будет виден при открытии подробной информации об услуге  |
|:SetPrice(**19.95**)|Устанавливает стоимось услуги в рублях|
|:SetTerm(**0**)|Устанавливает срок действия услуги в днях. Если указать **0 — услуга единоразовая**. **Если не указать — бесконечная**  |
|:SetCategory("**Категория**")|Устанавливает в какой категории будет отоброжатья услуга в главном меню. **Если не указать услуга будет отображаться в категории  "разное"**|

### Дополнительные методы
|Метод|Описание|
|-------|----|
|:SetImage("**http://site/img.png**")|Устаналивает ссылку на "**баннер**" услуги. Рекомендуемый размер 1000х400 или в этом соотношении. Отобразиться в инфе о товаре |
|:SetIcon("**http://site/img.png**")|Устанавливает **Иконку** в соотношении 1:1. Рекомендуемый размер 100 px|
|:SetHighlightColor(col)|Устанавливает **цвет текста** названию услуги|
|:SetDiscountedFrom(iOldPrice)|Устанавливает **старую цену** у услуги. Она будет отображаться зачеркнутой|
|:SetStackable(true)|**Разрешает покупку нескольких штук** (например, накопительные услуги, типа лимита пропов). **Использовать с SetTerm() != 0** |
|:SetNetworked(true)|Если игрок купил итем с этим методом, то он будет виден в **IGS.PlayerPurchases(LocalPlayer())** для этого игрока (другие итем не увидят. Для этого другое средство)|
|:SetCanBuy(function(pl, bGlobal) end)|Позволяет установить условие при котором игроки не смогут покупать товар.<br><br>**Пример:**<br><br>:SetCanBuy(function(pl, bGlobal)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if not pl:isPremium() then<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return "Чтобы купить это нужен премиум!"<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;end<br> end)
|:SetOnBuy(function(pl, bGlobal, iInvID) end)|Выполняется на сервере после покупки итема в инвентарь|
|:SetCanActivate(function(pl, global, invDbID) end)|Позволяет установить условие при котором игроки не смогут активировать товар из инвентаря.|
|:SetOnActivate(function(pl) end)|Выполняется на сервере перед активацией итема из инвентаря|
|:SetValidator(function(pl) end)|Выполняется при входе игрока на сервер.<br><br>Если условие возращает false выполняется :SetOnActivate|
|:SetMaxPlayerPurchases(num)|Устанавливает максимальное количество покупок услуги для игрока.<br><br>**Пример:**<br>При SetMaxPlayerPurchases(1) игрок сможет купить эту услугу только один раз, что полезно для тестовых випок.|
|:SetHidden(bool)|Скрывает предмет из меню, но сохраняет функционал для тех, у кого предмет числится в БД|
|:SetItems(items)|Позволяет предмету выдавать несколько других. items — таблица, в которой перечислены все выдаемые итемы (перед этим их нужно присвоить переменным)<br><br>**Пример:** :SetItems({VIP, VIP, VIP}) — выдает три випки|
|:SetRandom(items)|Аналог "рулетки". Активирует случайный предмет из таблицы|
|:SetGlobal(true)|Делает итем глобальным. Он будет активирован на всех серверах проекта|

### Методы связанные с ULX
|Метод|Описание|
|----|----|
|:SetULXGroup(group)|Выдача ULX привелегии|
|:SetULXCommandAccess(cmd)|Дает доступ к ULX команде.<br><br>**Пример:**<br>:SetULXCommandAccess("ulx model")|

### Другие админки
|Метод|Описание|
|----|----|
|:SetFAdminGroup(group)|Выдаст группу в системе  FAdmin.|
|:SetEvolveRank(group)|Выдаст группу в системе  Evolve.|
|:SetXAdminGroup(group)|Выдаст группу в системе  xAdmin|
|:SetBAdminGroup(group)|Выдаст группу в системе bAdmin|
|:SetSGGroup(group)|Выдаст группу в системе ServerGuard|
|:SetSAMGroup(group)|Выдаст группу в системе SAM Admin Mod|

### Методы связанные с DarkRP
|Метод|Описание|
|----|----|
|:SetDarkRPItem(sEntClass)|Если указать класс шипмента или энтити, итем станет доступным только за донат|
|:SetDarkRPTeam(iTeamID)|Если указать ID профы (пример: TEAM_MAYOR, TEAM_CP), профа станет доступна только тем, кто купил её за донат.|
|:SetDarkRPMoney(iSum)|При активации игроку будет выдана указанная сумма денег.|
|:DisablePlayerHunger()|Отключает голод у игрока.|

### Методы связанные с PointShop 2
|Метод|Описание|
|----|----|
|:SetPoints(iAmount)|Выдает обычные поинты| 
|:SetPremiumPoints(iAmount)|Выдает премиум поинты|

### Методы связанные с Leveling System
|Метод|Описание|
|----|----|
|:SetLevels(iAmount)|Добавляет указанное количество уровней|
|:SetEXP(iAmount)|Выдает опыт|

### Методы которые работают на всех гейммодах
|Метод|Описание|
|----|----|
|:SetTool(sToolName)|Разрешает юзать определенный tool (rope, winch, advdupe2) только донатерам и админам|
|:SetEntity(sEntClass)|Позволяет спавнить указанную энтити через спавн меню (Q)|
|:SetWeapon(sWepClass)|То же, но для пушек|
|:SetVehicle(sVehClass)|А это для машин|

### [Пример сложной конфигурации](https://gist.github.com/284608002faf5ff10525874b0225801e)
### Пример простой можно увидеть в базовом настройщике скрипта


# Хуки

### Shared
|Хук|Аргументы|Описание|
|----|----|----|
|IGS.OnServersLoaded|Без аргументов|Вызывается после получения информации о серверах вашего проекта, где еще работает автодонат. Если хук не вызовется, скрипт не загрузится|
|IGS.Initialized|Без аргументов|Вызывается после полной загрузки скрипта|
|IGS.OnSuccessPurchase|player _client_<br>table _ITEM_<br>boolean _isGlobal_<br>int _itemID_|Вызывается после успешной покупки предмета в магазине|
|IGS.OnFailedPurchase|player _client_<br>table _ITEM_<br>boolean _isGlobal_<br> string _error_|Вызывается после неудачной покупки предмета в магазине. Например, недостаточно денег или не прошла проверка :CanBuy|
|IGS.PaymentStatusUpdated|player _client_<br>table _status_| Вызывается после обновления статуса пополнения счета.<br>На клиенте первый аргумент (игрок) не передается. <br><br>Вид данных: https://img.qweqwe.ovh/1494089756498.png<br><br>**pay** - Деньги переведены.<br>**error** - Какая-то ошибка.<br>**check** - Игрок перешел к оплате| 
|IGS.PlayerPurchasesLoaded|player _client_<br>table _purchases_|После входа игрока на сервер с нашей системы начинают загружаться его покупки.<br>После завершения вызывается этот хук.<br>На клиенте первый аргумент (игрок) не передается. |
|IGS.OnSettingsUpdated|Без аргументов|Вызывается после получения или обновления данных для корректной работы функций IGS.GetMinCharge() и IGS.GetCurrencyPrice()|

### Server
|Хук|Аргументы|Описание|
|----|----|----|
|IGS.OnActivate|player _client_<br>table _ITEM_|Вызывается после успешной активации итема с инвентаря. Можно использовать для выдачи дополнительных бонусов|
|IGS.OnError. + method|string _error_<br>table _parameters_|Для опытных.<br>Вызывается в fetch.lua.<br> Предназначен для перехвата ошибок с определенных методов. <br><br>**Пример перехвата:**<br><br>hook.Add("IGS.OnError.servers.get", "servers.get.catchError", function(error, parameters)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;print("Ошибка: " .. error .. "\n Переданные параметры: " .. parameters .. "\n");<br> end)|
|IGS.CanPlayerActivateItem|player _client_<br>table _ITEM_<br>boolean _global_<br>int _invID_|Вызывается при активации игроком услуги. Должен возвращать true или false в зависимости от того, может ли игрок активировать услугу. Если возвращен false, надо указать причину.<br><br>**Пример:**<br>hook.Add("IGS.CanPlayerActivateItem", "OnlyAdminActivate", function(pl, item, global, invid)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if item:UID() == "admin_super_item" and !pl:IsAdmin() then<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return false, "Активация возможна только для админов!" <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;end<br>end)|
|IGS.CanPlayerBuyItem|player _client_<br>table _ITEM_<br>boolean _global_<br>int _invID_|Вызывается при покупки игроком услуги. Должен возвращать true или false в зависимости от того, может ли игрок купить услугу. Если возвращен false, надо указать причину.<br><br>**Пример:**<br>hook.Add("IGS.CanPlayerBuyItem", "OnlyAdminBuy", function(pl, item, global, invid)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if item:UID() == "admin_super_item" and !pl:IsAdmin() then<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return false, "Покупка возможна только для админов!" <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;end<br>end)|

### CLIENT:
|Хук|Аргументы|Описание|
|----|----|----|
|IGS.OnDepositWinOpen|int _depositAmount_|Вызывается при открытии окошка пополнения счета (Вот этого: https://img.qweqwe.ovh/1493842563826.png).<br> depositAmount - сумма для пополнения на которую открылась менюшка |
|IGS.OnItemInfoOpen|table _ITEM_|Вызывается при открытии этого окошка: https://img.qweqwe.ovh/1493843276142.png|
|IGS.CatchActivities|panel _activity_<br>panel _sidebar_|В хуке должен вызываться метод activity:AddTab("Название вкладки",Панель вкладки,"Путь к материалу иконки 32*32")|

**Если не хватает какого-то хука — скажите нам. Не добавляйте его сами**


# Остальное
* В транзакциях покупки начинаются с "P: "
* Активации купонов с "C: "
* Пополнения счета с "A: "
* Все операции с игроками проводятся по SteamID64 идентификатору (Никаких pl:SteamID())
* Избегай InitPostEntity и других хуков вроде loadCustomDarkRPItems при добавлении итемов в additems.lua, так как эти хуки могут проскочить из-за особенности загрузки скрипта.

***Вся остальная информация находится в комментариях к методам и функциям в коде, но я постараюсь вскоре перенести сюда.***

> Если в документации чего-то не хватает, то [обратитесь к нам](https://gm-donate.ru/support)

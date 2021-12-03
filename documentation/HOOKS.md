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

**Если не хватает какого-то хука -- скажите нам. Не добавляйте его сами**

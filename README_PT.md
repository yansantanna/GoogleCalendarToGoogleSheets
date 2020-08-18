# GoogleCalendarToGoogleSheets


Este código é para exportar dados do Google Agenda para planilhas do Google. Esta é a versão em português. Você pode alterar os parâmetros ache necessário. 

O objetivo de exportar os datos de Google Agenda a uma planilha de google é ter mais possibilidades de controle. É muito importante ter em mente que se deve usar o mesmo formato de preenchimento de em evento em Google Agenda, para que seja mais facil analisar os dados. 

A primeira coisa que você deve fazer é abrir uma planilha do google, ir a Ferramentas e clicar no "editor de scripts":

Copie e cole o código:
__________________________________________________________________________________________________________________________________________________________
function export_gcal_to_gsheet(){

var mycal = "micorreo@gmail.com"; var cal = CalendarApp.getCalendarById(mycal);

var events = cal.getEvents(new Date("January 01, 2020 00:00:00 CST"), new Date(), {search: '-project123'});

var sheet = SpreadsheetApp.getActiveSheet();

var header = [[ "Día de la Semana", "Fecha", "Titulo", "Dirección", "Descripción", "Creado por:"]] var range = sheet.getRange(1,1,1,6); range.setValues(header);

for (var i=0;i<events.length;i++) { var row=i+2;

var details=[[ getWeekDay(events[i].getStartTime()), events[i].getStartTime() , events[i].getTitle() , events[i].getLocation() , events[i].getDescription(), events[i].getCreators() ]]; var range=sheet.getRange(row,1,1,6); range.setValues(details); } }

function getWeekDay(date){ var dayNumber = date.getDay(); var days = ['Domingo','Lunes','Martes','Miércoles','Jueves','Viernes','Sabado']; return days[dayNumber]; }
_________________________________________________________________________________________________________________________________________________________
Execute o código.

Personalizações importantes:
Altere o ID do calendário a ser exportado, variável myCal:
var mycal = "mymail@gmail.com";

Para obter o ID abra o Google Calendar, no lado esquerdo procure o calendário, pressione os 3 pontos ("configurar e compartilhar") e em Integrar o calendário Ele estará no ID do calendário, copie e cole onde está "mymail@gmail.com" , com aspas.

Data de início e data de término:
var events = cal.getEvents(new Date("January 01, 2020 00:00:00 CST"), new Date(), {search: '-project123'});

A data de início é a primeira e a data de término é a segunda na linha de comando. É possível, por exemplo, pegar aqueles de 01/01/2019 a 18/08/2020. Para que isso seja possível, você deve alterar as datas na linha de código:

var events = cal.getEvents(new Date("January 01, 2019 00:00:00 CST"), new Date("August 18, 2020 23:59:59 CST"), {search: '-project123'});

Parâmetros do cabeçalho:
var header = [[ "Día de la Semana", "Fecha", "Titulo", "Dirección", "Descripción", "Creado por:"]] var range = sheet.getRange(1,1,1,6); range.setValues(header);

E

var details=[[ getWeekDay(events[i].getStartTime()), events[i].getStartTime() , events[i].getTitle() , events[i].getLocation() , events[i].getDescription(), events[i].getCreators() ]]; var range=sheet.getRange(row,1,1,6); range.setValues(details);

É importante observar que o cabeçalho da primeira parte deve estar de acordo com o parâmetro da segunda parte. Exemplo, "Dia da semana" = getWeekDay (events [i] .getStartTime ()), Date = events [i] .getStartTime (), etc ...

Além disso, se você quiser adicionar mais parâmetros, deve fazê-lo nas duas partes. Se você colocar mais um parâmetro, terá que alterar de 6 para 7 nas linhas do código var range = sheet.getRange (1,1,1,6); e var range = sheet.getRange (linha, 1,1,6); ou se você deseja remover, mude de 6 para 5.

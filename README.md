# GoogleCalendarToGoogleSheet
Este código es para exportar los datos de google calendar a google sheets. Esta es la versión en Castellano.
Es posible cambiar los parámetros para los que creas que son necesarios. El objetivo es tener más posibilidades para controlar tus datos de Google Calendar.
Es muy importante tener en cuenta que utilizar el mismo formato para rellenar tu google calendar es fundamental para futuros analisis de datos. 


Lo primero que debes hacer es abrir una hoja de calculo de google, en Herramientas hacer clic en editor de secuencias de comandos: 

Copiar y pegar el código:
_______________________________________________________________________________________________________________________________________________________
function export_gcal_to_gsheet(){


var mycal = "micorreo@gmail.com";
var cal = CalendarApp.getCalendarById(mycal);

var events = cal.getEvents(new Date("January 01, 2020 00:00:00 CST"), new Date(), {search: '-project123'});


var sheet = SpreadsheetApp.getActiveSheet();

var header = [[ "Día de la Semana", "Fecha", "Titulo", "Dirección", "Descripción", "Creado por:"]]
var range = sheet.getRange(1,1,1,6);
range.setValues(header);

  

for (var i=0;i<events.length;i++) {
  var row=i+2;

  var details=[[ getWeekDay(events[i].getStartTime()),  events[i].getStartTime() , events[i].getTitle() , events[i].getLocation() , events[i].getDescription(), events[i].getCreators() ]];
  var range=sheet.getRange(row,1,1,6);
  range.setValues(details);
 }
}


function getWeekDay(date){
  var dayNumber = date.getDay();
  var days = ['Domingo','Lunes','Martes','Miércoles','Jueves','Viernes','Sabado'];
  return days[dayNumber];
}
_________________________________________________________________________________________________________________________________________________________


Ejecutar el codigo.

## Personalizaciones importantes:

### Cambiar el ID del calendario que va a ser exportado, variable myCal:
var mycal = "micorreo@gmail.com";

Para obtener el ID abra Google Calendar, en el lado izquierdo busque el calendario, pulsa los 3 puntos("configurar y compartir") y en Integrar el calendario
Estará en ID del calendario, copie y pegue donde está "micorreo@gmail.com", con comillas. 


Fecha de inicio y Fecha fin:

var events = cal.getEvents(new Date("January 01, 2020 00:00:00 CST"), new Date(), {search: '-project123'});



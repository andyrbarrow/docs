Signal K filter
###############

.. image:: img/SKfilter2.png

What is Signal K Filter?
************************

The Signal K server wants to get all data it gets.

Why should we filter Signal K?

* Some devices send data which are always wrong (e.g. You can't disable unwanted sentences on a nmea 2000 bus, or a defective water temp sensor in the log on nmea 0183, or ...)
* You have a backup device (e.g. A second GPS or AIS)

To explain the problem we look at two GPS separated from each other on your boat.

If both GPS receivers are working properly, when you zoom your nautical chart your boat will seem to constantly zigzag as the Signal K server uses data from both GPS receivers. It could also be the case that you have one GPS receiver with bad reception. The Signal K server will still try to use the data from both receivers unless you filter the data from the unwanted GPS.

For both GPS receivers, the Signal K path will be identical but not the source.

The typical way to resolve this issue and use only a single GPS receiver would be to decide which source you intend to use for every Signal K path. As long as you are able to make this decision everything will be fine. (When you start converting nmea 2000 to nmea 0183 or the other way. Is there a chance to say only convert the Signal K path from a special source? No.)

The better solution is to filter the data before it gets into the Signal K server.

There are two ways to perform this action using the SK Filter app:

* FILTER: This is the hard way, as only Signal K paths which match the selected criteria are sent to the server. Paths with the same name from other sources will be ignored.
* PRIORITY: This is the better way to filter, as other sources can still be used. The selectrion criteria are the same, but if there is no communication from the priority source within a time limit (selectable timeout), any source for that Signal K path will be sent to the Signal K server. In this way the you have a fallback functionality

How does it work?
*****************

Signal K filter is based on the Signal K Node-RED library.

OpenPlotter does manage some Node-RED source code. A Node-RED flow page will be created with the name "OpenPlotter Filter". The filter code is put into subflows. These should not be edited in Node-RED - the SK Filter app should be used.

Below are two pictures of Signal K filter in Node-RED created by the SK Filter app.

.. image:: img/SKfilter_nodered1.png

This is how it looks in Node-RED.

.. image:: img/SKfilter_nodered2.png

This is the edit view for an opened subflow created by the OpenPlotter Signal K filter.


How can I determine the criteria?
*********************************

.. image:: img/SKfilter_Edit.png

In this picture you can see "Filter on Source" (criteria) to choose. In the following picture you see how SK Diagnostic shows you the available values.

.. image:: img/SKdiagnostic.png

.. tip::
	To find double Signal K path click on "Sort SK"

.. note::
	Signal K uses  ONLY  SI units!!! (rad, K, m, Hz, Pa, V, A, J, s)
	
	To make the values readable they are converted in SK Diagnostic. Unselect "Private Unit" to see real Signal K values. The "Unit setting" is only for SK Diagnostic "Private Unit" and nothing else.


Known issues
************

The Signal K server starts before Node-RED. A few seconds you will get data unfiltered.


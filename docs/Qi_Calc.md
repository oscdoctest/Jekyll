Qi Calculations
====================

The Qi Calculation APIs allow you to create custom calculations using JavaScript or TypeScript. Calculations can be scheduled to run  periodically or can be triggered whenever a particular input stream receives an event. 

 - Scheduled
     Run on periodic schedule.
 - Triggered
     Run whenever a particular input stream receives an event.


The Qi Calculation API is provided using the ``IQiCalculationService`` interface, which may be accessed via the ``QiService.GetCalculationService( )`` helper. For more information see `Qi Calculation API calls <https://qi-docs.readthedocs.org/en/latest/Qi_Calc_API.html>`__.

The following table shows the required and optional Qi calculation properties:

+---------------+------------------------------+-------------+--------------------------------------------+
| Property      | Type                         | Optionality |Details                                     |
+===============+==============================+=============+============================================+
| ID            | String                       | Required    | An Identifier for referencing the stream.  |
+---------------+------------------------------+-------------+--------------------------------------------+
| TypeId        | String                       | Required    | The type to be used for this stream.       |
+---------------+------------------------------+-------------+--------------------------------------------+
| Name          | String                       | Optional    | The name of the stream.                    |
+---------------+------------------------------+-------------+--------------------------------------------+
| Description   | String                       | Optional    | Text that describes the stream.            |
+---------------+------------------------------+-------------+--------------------------------------------+
| BehaviorId    | String                       | Optional    | The stream behavior for this stream.       |
+---------------+------------------------------+-------------+--------------------------------------------+
| Tag           | String                       | Optional    | A collection of strings that permit        |
|               |                              |             | classifying and identifying individual     |
|               |                              |             | streams.                                   |
+---------------+------------------------------+-------------+--------------------------------------------+
| Metadata      | iDictionary<string, string>  | Optional    | A dictionary for users to store information|
|               |                              |             | that is relevant to the stream             |
+---------------+------------------------------+-------------+--------------------------------------------+
| Indexes       | IList<QiStreamIndex>         | Optional    | Used to define secondary indexes for stream|
+---------------+------------------------------+-------------+--------------------------------------------+

**Restrictions and limitations**

*Qi calculation ID*

1. Is not case sensitive.
2. Can contain spaces.
3. Cannot start with two underscores ("\_\_").
4. Can contain a maximum of 260 characters.
5. Cannot use the following characters: ( / : ? # [ ] @ ! $ & ' ( ) \* +
   , ; = %)
6. Cannot start or end with a period.
7. Cannot contain consecutive periods.
8. Cannot consist of only periods. 


.. toctree::
   Qi_Calc_API

   
   


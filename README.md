# BIRT Runner
Private birt runner for MoE Project use only.

Run compile BIRT `.rptdesign` files from your laravel application application.

You can use the BIRT Designer to create reports, and save them as `.rptdesign` files and place into Report folder of your laravel project.
Then you can generate the reports from your laravel application and present them to your end user.

The reports can be generated in HTML, PDF, DOC, XLS, PPT and Postscript.

## How it works

This library is a clean wrapper around the `genReport.sh` shell-script which is part of the BIRT Runtime.
This means that you'll need to have the BIRT Runtime installed (see below).

## Prerequisites: BIRT Runtime

You'll need to have a recent version of the BIRT Runtime extracted somewhere on your computer/server.

You can download it here: [http://download.eclipse.org/birt/downloads/](http://download.eclipse.org/birt/downloads/)

Make sure you download the `BIRT Runtime`, and not the `All-in-One` or other options.

After downloading the file (birt-runtime-4.8.0-xxxx.zip), rename the extracted folder "bi" and place in your laravel project.


## Example usage from laravel

```
use BirtRunner\Renderer;
use BirtRunner\Report;
use BirtRunner\Parameter;

```
```\
$report = new Report();
$report->loadFilename(base_path() . '/reports/test.rptdesign);
$renderer = new Renderer();
$renderer->setBirtHome();


$parameters = array();
$parameters[] = new Parameter('param1', 'val1');
$parameters[] = new Parameter('param2', 'val2');

$report_filename = 'reportfilexxxx.pdf';

//save my report generated into laravel storage directory
$storage_path = storage_path('app/public/reports/');

$outputfilename = $storage_path . $report_filename;
$renderer->render($report, [], $outputfilename);


return view('viewname')->with(['reportFileName' => $report_filename]);


//in the view use $reportFileName
{{ asset('storage/reports/' . $reportFileName) }}
```

## link storage

This library includes an example console command to invoke the library. You can use it like this:

    php artisan storage:link 

Based on the file-extension of the output file it will automatically detect the format.

## License

MIT (see [LICENSE.md](LICENSE.md))

## Credit 
Thank to "Joost Faassen" git referance project.

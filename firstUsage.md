# First usage

## Set-up a new project
It is always good to create a new project, then change into this project. Afterwards, the creation of a few research tasks is suggested; these task can change. If you also want to also create subtasks inside the tasks that is plausible. Generally, set up the project structure first. You can change it using the edit function.

## Set-up samples
If you have samples, add them to the database. This allows you to link  them to measurements later, as those are included.
- Use descriptive names for your samples, because otherwise they are easily mixed up.

## Enter procedures
If you have procedures (SOP: Standard-Operating-Procedures) as text-files, then store them in a common subfolder of the PASTA folder, e.g. StandardOperatingProcedures which makes it easy to include them into the database.

Just add a new procedure; use the path (until the PASTA folder) as the name and the content will be included. You can use the tag #version_1 #v1 or ... to mark the current version of the procedure.

## Enter measurements
Just drag and drop raw measurement files in the corresponding project-task.  After dropping the files into the subfolder, use the "Scan" button in the project-view and let the software include measurements automatically. You are suggested to curate the measurements: grade the data e.g. #1, #2...#5 (these are tags). You can add, e.g. "nice data, but strange undulations". During curation you will be asked for sample and procedure, '--' leaves these fields empty.

**Important:** Automatic inclusion of measurement data requires that appropriate python extractors exist. There are a number of extractors for various files supplied. If you need another, write your own and just add it to the extractor directory with the correct filename. See (extractors)[extractors] for the full list and their options.

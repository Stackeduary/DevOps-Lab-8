# CI/CD with GitLab

This the project for [**Lab 08: CI/CD with GitLab**](https://courses.cs.ut.ee/2021/DevOps/fall/Main/Lab08) in DevOps course.
Please visit [here](https://courses.cs.ut.ee/2021/DevOps/fall/Main/Practicals) for more information.

The Project directory is as follows:
```
<root>
  |
  |--- index.html
  |--- README.md
  |--- Sendewicz
  |		|
  |		|-- webapp
  |		|	|
  |		|	|--- index.html
  |		|-- docker
  |		|	|
  |		|	|--- Dockerfile
  |		|-- src
  |		|	|
  |		|	|--- analyze_csv.py
  |		|-- csv_data
  |			|
  |			|--- L2A_Sendewicz.csv
  |
  |--- .gitlab-ci.yml
  |--- .gitlab-ci_Sendewicz.yml
  |--- csv_data
  		|
  		|--- <sensor1_name>.csv
  		|--- <sensor2_name>.csv
  		|--- ...
  		|--- <sensorn_name>.csv
```

Find your name and make sure that you are using only the assigned csv file.
| Filename        | Student Name   |
|-----------------|----------------|
| AktEN.csv       | Talvik         |
|  CO00011.csv    | Kivi           |
|  CO00013.csv    | Tark           |
|  CumEg1.csv     | Saan           |
|  CumVlm1.csv    | Roopärg        |
|  DCall.csv      | Kittask        |
|  DP.csv         | Jenk           |
|  EelKuu5.csv    | Vija           |
|  Efek.csv       | Surrage Reis   |
|  EnProdHour.csv | Rapur          |
|  Fl1.csv        | Loide          |
|  HetkL1.csv     | Papkov         |
|  HetkL1R.csv    | Everest        |
|  HetkL2.csv     | Matišinets     |
|  HetkL2R.csv    | Ganjušev       |
|  HetkL3.csv     | Reimann        |
|  KogEN22.csv    | Ramos Martinez |
|  KogEn.csv      | Paul           |
|  KogVoiR.csv    | Roosalu        |
|  L1A.csv        | Kolde          |
|  L2A.csv        | Sendewicz      |
|  L2L3V.csv      | Hallikas       |
|  L3A.csv        | Sapas          |
|  L3L1V.csv      | Keshi          |
|  Lux.csv        | Valiyev        |
|  PaevEN.csv     | Hashimov       |
|  Pwr1.csv       | Krylov         |
|  TE00.csv       | Jain           |
|  TEx.csv        | Chernetskyi    |
|  TEx1.csv       | Ando           |
|  TFl.csv        | Yavorskyi      |
|  TFl1.csv       | Kaliuzhnyi     |
|  TFrPrtW.csv    | Lohvina        |
|  TOa.csv        | Valdas         |
|  TRt1.csv       | Kuusik         |


# Troubleshooter
## Error-1
* In any stage, if you get error something like below:
  ```
  Running with gitlab-runner 14.4.0 (4b9e985a)
      on runner in GitLab vm in Etais LKZJLZiB
  Preparing the "shell" executor 00:00
  Using Shell executor...
  Preparing environment 00:00
  Running on gitlab.novalocal...
  Getting source from Git repository 00:01
  Fetching changes with git depth set to 50...
  Reinitialized existing Git repository in /home/gitlab-runner/builds/LKZJLZiB/0/dehury/git-ci-cd-test-project/.git/
  fatal: git fetch-pack: expected shallow list
  fatal: The remote end hung up unexpectedly
  Cleaning up project directory and file based variables 00:00
  ERROR: Job failed: exit status 1
  ```
### Possible Solution
* Go to your repo
* Go to `settings` -> `CI/CD` -> Expand `General pipelines` 
  * Check `git clone` strategy NOT `git fetch` strategy
  * Make `Git shallow clone = 0`

## Error-2
* If the gitlab-runner unable to issue any docker command, then this will throw similar to below error:
  ```
  <output omitted>
  Skipping Git submodules setup
  Executing "step_script" stage of the job script 00:00
  $ docker login -u dehury -p $gitlabpassword gitlab.cs.ut.ee:5050
  WARNING! Using --password via the CLI is insecure. Use --password-stdin.
  Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/auth": dial unix /var/run/docker.sock: connect: permission denied
  ```

### Possible Solution
* Login to the VM, where the gitlab-runner is running.
* Open terminal (not required if you are using ssh to login)
* Add the `gitlab-runner` user docker group and just restart the docker service.
  * `usermod -aG docker gitlab-runner`
  * `sudo service docker restart`


Refer the course page for the detailed information: https://courses.cs.ut.ee/2021/DevOps/fall/Main/Lab08

# OpenELIS Global 2

This is the OpenELIS rewrite onto Java Spring, and with all new technology and
features. Please see our [website](http://www.openelis-global.org/) for more
information.

You can find more information on how to set up OpenELIS at our
[docs page](http://docs.openelis-global.org/)

### CI Status

[![Maven Build Status](https://github.com/I-TECH-UW/OpenELIS-Global-2/actions/workflows/ci.yml/badge.svg)](https://github.com/I-TECH-UW/OpenELIS-Global-2/actions/workflows/ci.yml)

[![Publish OpenELIS WebApp Docker Image Status](https://github.com/I-TECH-UW/OpenELIS-Global-2/actions/workflows/publish-and-test.yml/badge.svg)](https://github.com/I-TECH-UW/OpenELIS-Global-2/actions/workflows/publish-and-test.yml)

[![End to End QA Tests Status](https://github.com/I-TECH-UW/OpenELIS-Global-2/actions/workflows/frontend-qa.yml/badge.svg)](https://github.com/I-TECH-UW/OpenELIS-Global-2/actions/workflows/frontend-qa.yml)

### For Implementers who Just want to run OpenELIS without Making any Code Changes

see [OpenELIS-Docker setup](https://github.com/I-TECH-UW/openelis-docker)

### Running OpenELIS in Docker For Devlopers with Intention of Making code Changes

#### Running docker compose With pre-released docker images

    docker-compose up -d

#### Running docker compose with docker images built directly from the source code

    docker-compose -f build.docker-compose.yml up -d --build

#### Running docker compose With locally compiled/built Artifacts (ie the War file and React code) For Developers

1.  Fork the
    [OpenELIS-Global Repository](https://github.com/I-TECH-UW/OpenELIS-Global-2.git)
    and clone the forked repo. The `username` below is the `username` of your
    Github profile.

         git clone https://github.com/username/OpenELIS-Global-2.git

2.  innitialize and build sub modules

        cd OpenELIS-Global-2
        git submodule update --init --recursive
        cd dataexport
        mvn clean install -DskipTests

3.  Build the War file

          cd ..
          mvn clean install -DskipTests

4.  Start the containers to mount the locally compiled artifacts

        docker-compose -f dev.docker-compose.yml up -d

    Note : For Reflecting Local changes in the Running Containers ;

- Any Changes to the [Front-end](./frontend/) React Source Code will be directly
  Hot Reloaded in the UI
- For changes to the [Back-end](./src/) Java Source code

  - Run the maven build again to re-build the War file

         mvn clean install -DskipTests

  - Recreate the Openelis webapp container

        docker-compose -f dev.docker-compose.yml up -d  --no-deps --force-recreate oe.openelis.org

#### The Instaces can be accesed at

| Instance     |                   URL                   | credentials (user : password) |
| ------------ | :-------------------------------------: | ----------------------------: |
| Legacy UI    | https://localhost/api/OpenELIS-Global/  |            admin: adminADMIN! |
| New React UI |           https://localhost/            |            admin: adminADMIN! |

**Note:** If your browser indicates that the website is not secure after
accessing any of these links, simply follow these steps:

1. Scroll down on the warning page.
2. Click on the "Advanced" button.
3. Finally, click on "Proceed to https://localhost" to access the development
   environment.

#### Formating the Source code after making changes

1.  After making UI changes to the [frontend](./frontend/) directory , run the
    formatter to properly format the Frontend code

        cd frontend
        npm run format

2.  After making changes to the [backend](./src/) directory, run the formatter
    to properly format the Java code

        mvn spotless:apply

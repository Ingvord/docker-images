FROM mliszcz/tango-cs:xenial

RUN wget http://downloads.sourceforge.net/project/tango-cs/tango-9.2.2.tar.gz

RUN tar xf tango-9.2.2.tar.gz

RUN mkdir -p dbinit/include

RUN cp tango-9.2.2/cppserver/database/create_db.sql.in dbinit/create_db.sql

RUN cp tango-9.2.2/cppserver/database/create_db_tables.sql.in dbinit/include/create_db_tables.sql

RUN cp tango-9.2.2/cppserver/database/stored_proc.sql.in dbinit/include/stored_proc.sql

RUN sed -i "s|@TANGO_DB_NAME@|tango_db|g" dbinit/create_db.sql

RUN sed -i "s|@TANGO_DB_NAME@|tango_db|g" dbinit/include/create_db_tables.sql

RUN sed -i "s|@TANGO_DB_NAME@|tango_db|g" dbinit/include/stored_proc.sql

RUN sed -i "s|^source create_db_tables.sql$|source /docker-entrypoint-initdb.d/include/create_db_tables.sql|g" dbinit/create_db.sql

RUN sed -i "s|^source stored_proc.sql$|source /docker-entrypoint-initdb.d/include/stored_proc.sql|g" dbinit/create_db.sql

RUN sed -i "/CREATE DATABASE tango_db;/d" dbinit/create_db.sql


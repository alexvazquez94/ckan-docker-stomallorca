FROM ckan/ckan-base:2.10.1

# Set up environment variables
ENV APP_DIR=/srv/app
ENV SRC_EXTENSIONS_DIR=/srv/app/src_extensions

# Set timezone
ARG TZ
RUN echo ${TZ} > /etc/timezone

# Make sure both files are not exactly the same
RUN if ! [ /usr/share/zoneinfo/${TZ} -ef /etc/localtime ]; then \
        cp /usr/share/zoneinfo/${TZ} /etc/localtime ;\
    fi ;

# Install plugin's
### Harvester ###
RUN apk --update add redis
RUN pip3 install -e 'git+https://github.com/ckan/ckanext-harvest.git@master#egg=ckanext-harvest' && \
    pip3 install -r https://raw.githubusercontent.com/ckan/ckanext-harvest/master/requirements.txt

### Scheming ###
RUN  pip3 install -e 'git+https://github.com/ckan/ckanext-scheming.git@master#egg=ckanext-scheming'

### Pages ###
RUN  pip3 install -e git+https://github.com/ckan/ckanext-pages.git#egg=ckanext-pages

### DCAT ###
RUN  pip3 install -e git+https://github.com/ckan/ckanext-dcat.git@v1.5.1#egg=ckanext-dcat && \
     pip3 install -r https://raw.githubusercontent.com/ckan/ckanext-dcat/v1.5.1/requirements.txt
	 
### Fluent ###
RUN pip3 install -e git+https://github.com/ckan/ckanext-fluent.git@master#egg=ckanext-fluent && \ 
    pip3 install -r https://raw.githubusercontent.com/ckan/ckanext-fluent/master/requirements.txt
	
### STO Mallorca theming ###
RUN  pip3 install -e git+https://github.com/alexvazquez94/ckanext-stomallorca_theme.git@master#egg=ckanext-stomallorca_theme && \
     pip3 install -r https://raw.githubusercontent.com/alexvazquez94/ckanext-stomallorca_theme/master/requirements.txt	

# Copy start_ckan.sh for the configuration and startup of CKAN
COPY setup/start_ckan.sh.override ${APP_DIR}/start_ckan.sh
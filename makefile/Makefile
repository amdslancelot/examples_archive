SHELL = /bin/bash

tempdir := $(shell mktemp -d -p /var/tmp 2>/dev/null)
workdir := $(PWD)

all: file-list-before-build puppet-agent-7.18.0-1.x86_64.rpm

puppet-agent-7.18.0-1.x86_64.rpm: puppet-agent-7.18.0.tar.gz
	bash -c 'mkdir -p $(tempdir)/rpmbuild/{SOURCES,SPECS,BUILD,RPMS,SRPMS}'
	cp puppet-agent-7.18.0.tar.gz $(tempdir)/rpmbuild/SOURCES
	cp file-list-for-rpm $(tempdir)/rpmbuild/SOURCES
	cp puppet-agent.spec $(tempdir)/rpmbuild/SPECS
	PATH=/opt/freeware/bin:$$PATH /usr/bin/rpmbuild -bb --target x86_64 --define '_topdir $(tempdir)/rpmbuild' --define 'dist .el8' $(tempdir)/rpmbuild/SPECS/puppet-agent.spec
	mkdir -p output/el/8/puppet7/x86_64
	cp $(tempdir)/rpmbuild/*RPMS/**/*.rpm ./output/el/8/puppet7/x86_64

file-list-before-build:
	(find -H "/opt/puppetlabs" "/opt/puppetlabs/puppet" "/etc/puppetlabs" "/opt/puppetlabs/bin" "/var/log/puppetlabs" "/run/puppetlabs" "/opt/puppetlabs/puppet/cache" "/opt/puppetlabs/puppet/public" "/etc/puppetlabs/puppet" "/opt/puppetlabs/puppet/share/locale" "/etc/puppetlabs/code" "/etc/puppetlabs/code/modules" "/opt/puppetlabs/puppet/modules" "/etc/puppetlabs/code/environments" "/etc/puppetlabs/code/environments/production" "/etc/puppetlabs/code/environments/production/manifests" "/etc/puppetlabs/code/environments/production/modules" "/etc/puppetlabs/code/environments/production/data" "/var/log/puppetlabs/puppet" "/opt/puppetlabs/facter/facts.d" "/opt/puppetlabs/puppet/vendor_modules" 2>/dev/null || find "/opt/puppetlabs" "/opt/puppetlabs/puppet" "/etc/puppetlabs" "/opt/puppetlabs/bin" "/var/log/puppetlabs" "/run/puppetlabs" "/opt/puppetlabs/puppet/cache" "/opt/puppetlabs/puppet/public" "/etc/puppetlabs/puppet" "/opt/puppetlabs/puppet/share/locale" "/etc/puppetlabs/code" "/etc/puppetlabs/code/modules" "/opt/puppetlabs/puppet/modules" "/etc/puppetlabs/code/environments" "/etc/puppetlabs/code/environments/production" "/etc/puppetlabs/code/environments/production/manifests" "/etc/puppetlabs/code/environments/production/modules" "/etc/puppetlabs/code/environments/production/data" "/var/log/puppetlabs/puppet" "/opt/puppetlabs/facter/facts.d" "/opt/puppetlabs/puppet/vendor_modules" 2>/dev/null) | sort | uniq > file-list-before-build

file-list-after-build: puppet-runtime puppet facter hiera puppet-resource_api shellpath wrapper-script module-puppetlabs-augeas_core module-puppetlabs-cron_core module-puppetlabs-host_core module-puppetlabs-mount_core module-puppetlabs-scheduled_task module-puppetlabs-selinux_core module-puppetlabs-sshkeys_core module-puppetlabs-yumrepo_core module-puppetlabs-zfs_core module-puppetlabs-zone_core cleanup pl-ruby-patch
	(find -H "/opt/puppetlabs" "/opt/puppetlabs/puppet" "/etc/puppetlabs" "/opt/puppetlabs/bin" "/var/log/puppetlabs" "/run/puppetlabs" "/opt/puppetlabs/puppet/cache" "/opt/puppetlabs/puppet/public" "/etc/puppetlabs/puppet" "/opt/puppetlabs/puppet/share/locale" "/etc/puppetlabs/code" "/etc/puppetlabs/code/modules" "/opt/puppetlabs/puppet/modules" "/etc/puppetlabs/code/environments" "/etc/puppetlabs/code/environments/production" "/etc/puppetlabs/code/environments/production/manifests" "/etc/puppetlabs/code/environments/production/modules" "/etc/puppetlabs/code/environments/production/data" "/var/log/puppetlabs/puppet" "/opt/puppetlabs/facter/facts.d" "/opt/puppetlabs/puppet/vendor_modules" 2>/dev/null || find "/opt/puppetlabs" "/opt/puppetlabs/puppet" "/etc/puppetlabs" "/opt/puppetlabs/bin" "/var/log/puppetlabs" "/run/puppetlabs" "/opt/puppetlabs/puppet/cache" "/opt/puppetlabs/puppet/public" "/etc/puppetlabs/puppet" "/opt/puppetlabs/puppet/share/locale" "/etc/puppetlabs/code" "/etc/puppetlabs/code/modules" "/opt/puppetlabs/puppet/modules" "/etc/puppetlabs/code/environments" "/etc/puppetlabs/code/environments/production" "/etc/puppetlabs/code/environments/production/manifests" "/etc/puppetlabs/code/environments/production/modules" "/etc/puppetlabs/code/environments/production/data" "/var/log/puppetlabs/puppet" "/opt/puppetlabs/facter/facts.d" "/opt/puppetlabs/puppet/vendor_modules" 2>/dev/null) | sort | uniq > file-list-after-build

puppet-agent-7.18.0.tar.gz: file-list 
	mkdir -p 'puppet-agent-7.18.0'
	'tar' -cf - -T "file-list" "bill-of-materials" "/opt/puppetlabs/puppet/VERSION" "/usr/lib/systemd/system/puppet.service" "/opt/puppetlabs/puppet/bin/eyaml" "/opt/puppetlabs/puppet/lib/ruby/gems/2.7.0/specifications/puppet-7.18.0.gemspec" "/opt/puppetlabs/puppet/lib/ruby/gems/2.7.0/specifications/facter-4.2.11.gemspec" "/opt/puppetlabs/puppet/lib/ruby/gems/2.7.0/specifications/hiera-3.10.0.gemspec" "/etc/profile.d/puppet-agent.sh" "/etc/profile.d/puppet-agent.csh" "/opt/puppetlabs/puppet/bin/wrapper.sh" "/opt/puppetlabs/bin/facter" "/opt/puppetlabs/bin/hiera" "/opt/puppetlabs/bin/puppet" "/opt/puppetlabs/bin/pxp-agent" "/etc/sysconfig/puppet" "/usr/lib/tmpfiles.d/puppet-agent.conf" "/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/ftdetect/puppet.vim" "/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/ftplugin/puppet.vim" "/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/indent/puppet.vim" "/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/syntax/puppet.vim" "/etc/puppetlabs/puppet/puppet.conf" "/etc/puppetlabs/code/environments/production/environment.conf" "/etc/puppetlabs/code/environments/production/hiera.yaml" "/etc/puppetlabs/puppet/hiera.yaml" | ( cd 'puppet-agent-7.18.0/'; 'tar' xfp -)
	'tar' -cf - puppet-agent-7.18.0/ | gzip -9c > puppet-agent-7.18.0.tar.gz

file-list: file-list-before-build puppet-agent-project
	comm -23 file-list-after-build file-list-before-build > file-list
	comm -23 file-list-after-build file-list-before-build | sed -e 's/\(^.*[[:space:]].*$$\)/"\1"/g' > file-list-for-rpm

/opt/puppetlabs/puppet/VERSION:
	echo 7.18.0 > '/opt/puppetlabs/puppet/VERSION'

/opt/puppetlabs: file-list-before-build
	mkdir -p '/opt/puppetlabs'
/opt/puppetlabs/puppet: file-list-before-build
	mkdir -p '/opt/puppetlabs/puppet'
/etc/puppetlabs: file-list-before-build
	mkdir -p '/etc/puppetlabs'
/opt/puppetlabs/bin: file-list-before-build
	mkdir -p '/opt/puppetlabs/bin'
/var/log/puppetlabs: file-list-before-build
	mkdir -p '/var/log/puppetlabs'
/run/puppetlabs: file-list-before-build
	mkdir -p '/run/puppetlabs'
/opt/puppetlabs/puppet/cache: file-list-before-build
	mkdir -p '/opt/puppetlabs/puppet/cache'
/opt/puppetlabs/puppet/public: file-list-before-build
	mkdir -p '/opt/puppetlabs/puppet/public'
/etc/puppetlabs/puppet: file-list-before-build
	mkdir -p '/etc/puppetlabs/puppet'
/opt/puppetlabs/puppet/share/locale: file-list-before-build
	mkdir -p '/opt/puppetlabs/puppet/share/locale'
/etc/puppetlabs/code: file-list-before-build
	mkdir -p '/etc/puppetlabs/code'
/etc/puppetlabs/code/modules: file-list-before-build
	mkdir -p '/etc/puppetlabs/code/modules'
/opt/puppetlabs/puppet/modules: file-list-before-build
	mkdir -p '/opt/puppetlabs/puppet/modules'
/etc/puppetlabs/code/environments: file-list-before-build
	mkdir -p '/etc/puppetlabs/code/environments'
/etc/puppetlabs/code/environments/production: file-list-before-build
	mkdir -p '/etc/puppetlabs/code/environments/production'
/etc/puppetlabs/code/environments/production/manifests: file-list-before-build
	mkdir -p '/etc/puppetlabs/code/environments/production/manifests'
/etc/puppetlabs/code/environments/production/modules: file-list-before-build
	mkdir -p '/etc/puppetlabs/code/environments/production/modules'
/etc/puppetlabs/code/environments/production/data: file-list-before-build
	mkdir -p '/etc/puppetlabs/code/environments/production/data'
/var/log/puppetlabs/puppet: file-list-before-build
	mkdir -p '/var/log/puppetlabs/puppet'
/opt/puppetlabs/facter/facts.d: file-list-before-build
	mkdir -p '/opt/puppetlabs/facter/facts.d'
/opt/puppetlabs/puppet/vendor_modules: file-list-before-build
	mkdir -p '/opt/puppetlabs/puppet/vendor_modules'

puppet-agent-project: /opt/puppetlabs /opt/puppetlabs/puppet /etc/puppetlabs /opt/puppetlabs/bin /var/log/puppetlabs /run/puppetlabs /opt/puppetlabs/puppet/cache /opt/puppetlabs/puppet/public /etc/puppetlabs/puppet /opt/puppetlabs/puppet/share/locale /etc/puppetlabs/code /etc/puppetlabs/code/modules /opt/puppetlabs/puppet/modules /etc/puppetlabs/code/environments /etc/puppetlabs/code/environments/production /etc/puppetlabs/code/environments/production/manifests /etc/puppetlabs/code/environments/production/modules /etc/puppetlabs/code/environments/production/data /var/log/puppetlabs/puppet /opt/puppetlabs/facter/facts.d /opt/puppetlabs/puppet/vendor_modules /opt/puppetlabs/puppet/VERSION file-list-after-build
	touch puppet-agent-project

puppet-runtime: puppet-runtime-install

puppet-runtime-install:
	gunzip -c agent-runtime-7.18.0-202208121.el-8-x86_64.tar.gz | tar -k -C / -xf -
	touch puppet-runtime-install

puppet-runtime-clean:
	[ -d agent-runtime-7.18.0-202208121.el-8-x86_64 ] && cd agent-runtime-7.18.0-202208121.el-8-x86_64 && /usr/bin/make clean
	[ -e puppet-runtime-configure ] && rm puppet-runtime-configure
	[ -e puppet-runtime-build ] && rm puppet-runtime-build
	[ -e puppet-runtime-install ] && rm puppet-runtime-install

puppet-runtime-clobber: puppet-runtime-clean
	[ -d agent-runtime-7.18.0-202208121.el-8-x86_64 ] && rm -r agent-runtime-7.18.0-202208121.el-8-x86_64
	[ -e puppet-runtime-unpack ] && rm puppet-runtime-unpack

puppet: puppet-install

puppet-unpack: file-list-before-build
	: nothing to extract && \
	: nothing to extract && \
	: nothing to extract && \
	: nothing to extract
	touch puppet-unpack

puppet-patch: puppet-unpack
	touch puppet-patch

puppet-configure: puppet-patch puppet-runtime facter hiera
	[ -d puppet ] || mkdir -p puppet
	cd puppet && \
	for dir in ./locales/*/ ; do [ -d "$${dir}" ] || continue ; [ -d "$${dir}/LC_MESSAGES" ] || /bin/mkdir "$${dir}/LC_MESSAGES" ; msgfmt "$${dir}/puppet.po" -o "$${dir}/LC_MESSAGES/puppet.mo" ; done ;
	touch puppet-configure

puppet-build: puppet-configure
	cd puppet && \
	echo 'd /run/puppetlabs 0755 root root -' > puppet-agent.conf
	touch puppet-build

puppet-check: puppet-build
	touch puppet-check

puppet-install: puppet-check
	cd puppet && \
	install -d '/usr/lib/systemd/system' && \
	cp -p 'ext/systemd/puppet.service' '/usr/lib/systemd/system/puppet.service' && \
	chmod 0644 '/usr/lib/systemd/system/puppet.service' && \
	install -d '/etc/sysconfig' && \
	cp -p 'ext/redhat/client.sysconfig' '/etc/sysconfig/puppet' && \
	chmod 0644 '/etc/sysconfig/puppet' && \
	install -d '/usr/lib/tmpfiles.d' && \
	cp -p 'puppet-agent.conf' '/usr/lib/tmpfiles.d/puppet-agent.conf' && \
	chmod 0644 '/usr/lib/tmpfiles.d/puppet-agent.conf' && \
	/opt/puppetlabs/puppet/bin/ruby install.rb --ruby=/opt/puppetlabs/puppet/bin/ruby --no-check-prereqs --bindir=/opt/puppetlabs/puppet/bin --configdir=/etc/puppetlabs/puppet --sitelibdir=/opt/puppetlabs/puppet/lib/ruby/vendor_ruby --codedir=/etc/puppetlabs/code --vardir=/opt/puppetlabs/puppet/cache --publicdir=/opt/puppetlabs/puppet/public --rundir=/run/puppetlabs --logdir=/var/log/puppetlabs --localedir=/opt/puppetlabs/puppet/share/locale --configs --quick --no-batch-files --man --mandir=/opt/puppetlabs/puppet/share/man && \
	install -d '/opt/puppetlabs/puppet/bin' && \
	([[ '/opt/puppetlabs/puppet/bin/eyaml' -ef '/opt/puppetlabs/puppet/lib/ruby/vendor_gems/bin/eyaml' ]] || ln -s '/opt/puppetlabs/puppet/lib/ruby/vendor_gems/bin/eyaml' '/opt/puppetlabs/puppet/bin/eyaml') && \
	install -d '/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/ftdetect' && \
	cp -p '../ftdetect_puppet.vim' '/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/ftdetect/puppet.vim' && \
	chmod 0644 '/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/ftdetect/puppet.vim' && \
	install -d '/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/ftplugin' && \
	cp -p '../ftplugin_puppet.vim' '/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/ftplugin/puppet.vim' && \
	chmod 0644 '/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/ftplugin/puppet.vim' && \
	install -d '/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/indent' && \
	cp -p '../indent_puppet.vim' '/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/indent/puppet.vim' && \
	chmod 0644 '/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/indent/puppet.vim' && \
	install -d '/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/syntax' && \
	cp -p '../syntax_puppet.vim' '/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/syntax/puppet.vim' && \
	chmod 0644 '/opt/puppetlabs/puppet/share/vim/puppet-vimfiles/syntax/puppet.vim' && \
	install -d '/opt/puppetlabs/puppet/lib/ruby/gems/2.7.0/specifications' && \
	cp -p '.gemspec' '/opt/puppetlabs/puppet/lib/ruby/gems/2.7.0/specifications/puppet-7.18.0.gemspec' && \
	chmod 0644 '/opt/puppetlabs/puppet/lib/ruby/gems/2.7.0/specifications/puppet-7.18.0.gemspec' && \
	install -d -m '0750' '/opt/puppetlabs/puppet/cache' && \
	install -d -m '0755' '/opt/puppetlabs/puppet/public' && \
	install -d '/etc/puppetlabs/puppet' && \
	install -d '/opt/puppetlabs/puppet/share/locale' && \
	install -d '/etc/puppetlabs/code' && \
	install -d '/etc/puppetlabs/code/modules' && \
	install -d '/opt/puppetlabs/puppet/modules' && \
	install -d '/etc/puppetlabs/code/environments' && \
	install -d '/etc/puppetlabs/code/environments/production' && \
	install -d '/etc/puppetlabs/code/environments/production/manifests' && \
	install -d '/etc/puppetlabs/code/environments/production/modules' && \
	install -d '/etc/puppetlabs/code/environments/production/data' && \
	install -d '/etc/puppetlabs/code/environments/production' && \
	cp -p 'conf/environment.conf' '/etc/puppetlabs/code/environments/production/environment.conf' && \
	chmod 0644 '/etc/puppetlabs/code/environments/production/environment.conf' && \
	install -d -m '0750' '/var/log/puppetlabs/puppet' && \
	install -d '/etc/puppetlabs/code/environments/production' && \
	cp -p 'ext/hiera/hiera.yaml' '/etc/puppetlabs/code/environments/production/hiera.yaml' && \
	chmod 0644 '/etc/puppetlabs/code/environments/production/hiera.yaml'
	touch puppet-install

puppet-clean:
	[ -d puppet ] && cd puppet && /usr/bin/make clean
	[ -e puppet-configure ] && rm puppet-configure
	[ -e puppet-build ] && rm puppet-build
	[ -e puppet-install ] && rm puppet-install

puppet-clobber: puppet-clean
	[ -d puppet ] && rm -r puppet
	[ -e puppet-unpack ] && rm puppet-unpack

facter: facter-install

facter-unpack: file-list-before-build
	
	touch facter-unpack

facter-patch: facter-unpack
	touch facter-patch

facter-configure: facter-patch puppet-runtime pl-ruby-patch
	[ -d facter ] || mkdir -p facter
	touch facter-configure

facter-build: facter-configure
	touch facter-build

facter-check: facter-build
	touch facter-check

facter-install: facter-check
	cd facter && \
	/opt/puppetlabs/puppet/bin/ruby install.rb --no-batch-files --no-configs --bindir=/opt/puppetlabs/puppet/bin --sitelibdir=/opt/puppetlabs/puppet/lib/ruby/vendor_ruby --mandir=/opt/puppetlabs/puppet/share/man --ruby=/opt/puppetlabs/puppet/bin/ruby && \
	install -d '/opt/puppetlabs/puppet/lib/ruby/gems/2.7.0/specifications' && \
	cp -p 'facter.gemspec' '/opt/puppetlabs/puppet/lib/ruby/gems/2.7.0/specifications/facter-4.2.11.gemspec' && \
	chmod 0644 '/opt/puppetlabs/puppet/lib/ruby/gems/2.7.0/specifications/facter-4.2.11.gemspec' && \
	install -d '/opt/puppetlabs/facter/facts.d'
	touch facter-install

facter-clean:
	[ -d facter ] && cd facter && /usr/bin/make clean
	[ -e facter-configure ] && rm facter-configure
	[ -e facter-build ] && rm facter-build
	[ -e facter-install ] && rm facter-install

facter-clobber: facter-clean
	[ -d facter ] && rm -r facter
	[ -e facter-unpack ] && rm facter-unpack

hiera: hiera-install

hiera-unpack: file-list-before-build
	
	touch hiera-unpack

hiera-patch: hiera-unpack
	touch hiera-patch

hiera-configure: hiera-patch puppet-runtime
	[ -d hiera ] || mkdir -p hiera
	touch hiera-configure

hiera-build: hiera-configure
	touch hiera-build

hiera-check: hiera-build
	touch hiera-check

hiera-install: hiera-check
	cd hiera && \
	/opt/puppetlabs/puppet/bin/ruby install.rb --configs --configdir=/etc/puppetlabs/puppet --man --mandir=/opt/puppetlabs/puppet/share/man --no-batch-files --no-configs --bindir=/opt/puppetlabs/puppet/bin --sitelibdir=/opt/puppetlabs/puppet/lib/ruby/vendor_ruby --ruby=/opt/puppetlabs/puppet/bin/ruby && \
	install -d '/opt/puppetlabs/puppet/lib/ruby/gems/2.7.0/specifications' && \
	cp -p '.gemspec' '/opt/puppetlabs/puppet/lib/ruby/gems/2.7.0/specifications/hiera-3.10.0.gemspec' && \
	chmod 0644 '/opt/puppetlabs/puppet/lib/ruby/gems/2.7.0/specifications/hiera-3.10.0.gemspec'
	touch hiera-install

hiera-clean:
	[ -d hiera ] && cd hiera && /usr/bin/make clean
	[ -e hiera-configure ] && rm hiera-configure
	[ -e hiera-build ] && rm hiera-build
	[ -e hiera-install ] && rm hiera-install

hiera-clobber: hiera-clean
	[ -d hiera ] && rm -r hiera
	[ -e hiera-unpack ] && rm hiera-unpack

puppet-resource_api: puppet-resource_api-install

puppet-resource_api-unpack: file-list-before-build
	export GEM_HOME="/opt/puppetlabs/puppet/lib/ruby/vendor_gems" && \
	export RUBYLIB="/opt/puppetlabs/puppet/lib/ruby/vendor_ruby:$(RUBYLIB)"
	touch puppet-resource_api-unpack

puppet-resource_api-patch: puppet-resource_api-unpack
	touch puppet-resource_api-patch

puppet-resource_api-configure: puppet-resource_api-patch puppet-runtime
	[ -d puppet-resource_api ] || mkdir -p puppet-resource_api
	touch puppet-resource_api-configure

puppet-resource_api-build: puppet-resource_api-configure
	export GEM_HOME="/opt/puppetlabs/puppet/lib/ruby/vendor_gems" && \
	export RUBYLIB="/opt/puppetlabs/puppet/lib/ruby/vendor_ruby:$(RUBYLIB)" && \
	cd puppet-resource_api && \
	/opt/puppetlabs/puppet/bin/gem build puppet-resource_api.gemspec
	touch puppet-resource_api-build

puppet-resource_api-check: puppet-resource_api-build
	touch puppet-resource_api-check

puppet-resource_api-install: puppet-resource_api-check
	export GEM_HOME="/opt/puppetlabs/puppet/lib/ruby/vendor_gems" && \
	export RUBYLIB="/opt/puppetlabs/puppet/lib/ruby/vendor_ruby:$(RUBYLIB)" && \
	cd puppet-resource_api && \
	/opt/puppetlabs/puppet/bin/gem install --no-document --local puppet-resource_api-*.gem
	touch puppet-resource_api-install

puppet-resource_api-clean:
	[ -d puppet-resource_api ] && cd puppet-resource_api && /usr/bin/make clean
	[ -e puppet-resource_api-configure ] && rm puppet-resource_api-configure
	[ -e puppet-resource_api-build ] && rm puppet-resource_api-build
	[ -e puppet-resource_api-install ] && rm puppet-resource_api-install

puppet-resource_api-clobber: puppet-resource_api-clean
	[ -d puppet-resource_api ] && rm -r puppet-resource_api
	[ -e puppet-resource_api-unpack ] && rm puppet-resource_api-unpack

shellpath: shellpath-install

shellpath-unpack: file-list-before-build
	: no source, so nothing to extract && \
	: nothing to extract && \
	: nothing to extract
	touch shellpath-unpack

shellpath-patch: shellpath-unpack
	touch shellpath-patch

shellpath-configure: shellpath-patch
	[ -d ./ ] || mkdir -p ./
	touch shellpath-configure

shellpath-build: shellpath-configure
	touch shellpath-build

shellpath-check: shellpath-build
	touch shellpath-check

shellpath-install: shellpath-check
	cd ./ && \
	install -d '/etc/profile.d' && \
	cp -p './puppet-agent.sh' '/etc/profile.d/puppet-agent.sh' && \
	chmod 0644 '/etc/profile.d/puppet-agent.sh' && \
	install -d '/etc/profile.d' && \
	cp -p './puppet-agent.csh' '/etc/profile.d/puppet-agent.csh' && \
	chmod 0644 '/etc/profile.d/puppet-agent.csh'
	touch shellpath-install

shellpath-clean:
	[ -d ./ ] && cd ./ && /usr/bin/make clean
	[ -e shellpath-configure ] && rm shellpath-configure
	[ -e shellpath-build ] && rm shellpath-build
	[ -e shellpath-install ] && rm shellpath-install

shellpath-clobber: shellpath-clean
	[ -d ./ ] && rm -r ./
	[ -e shellpath-unpack ] && rm shellpath-unpack

wrapper-script: wrapper-script-install

wrapper-script-unpack: file-list-before-build
	: no source, so nothing to extract && \
	: nothing to extract && \
	: nothing to extract && \
	: nothing to extract
	touch wrapper-script-unpack

wrapper-script-patch: wrapper-script-unpack
	touch wrapper-script-patch

wrapper-script-configure: wrapper-script-patch
	[ -d ./ ] || mkdir -p ./
	touch wrapper-script-configure

wrapper-script-build: wrapper-script-configure
	touch wrapper-script-build

wrapper-script-check: wrapper-script-build
	touch wrapper-script-check

wrapper-script-install: wrapper-script-check
	cd ./ && \
	install -d '/opt/puppetlabs/puppet/bin' && \
	cp -p 'sysv-wrapper.sh' '/opt/puppetlabs/puppet/bin/wrapper.sh' && \
	chmod 0755 '/opt/puppetlabs/puppet/bin/wrapper.sh' && \
	install -d '/opt/puppetlabs/bin' && \
	([[ '/opt/puppetlabs/bin/facter' -ef '/opt/puppetlabs/puppet/bin/wrapper.sh' ]] || ln -s '/opt/puppetlabs/puppet/bin/wrapper.sh' '/opt/puppetlabs/bin/facter') && \
	install -d '/opt/puppetlabs/bin' && \
	([[ '/opt/puppetlabs/bin/hiera' -ef '/opt/puppetlabs/puppet/bin/wrapper.sh' ]] || ln -s '/opt/puppetlabs/puppet/bin/wrapper.sh' '/opt/puppetlabs/bin/hiera') && \
	install -d '/opt/puppetlabs/bin' && \
	([[ '/opt/puppetlabs/bin/puppet' -ef '/opt/puppetlabs/puppet/bin/wrapper.sh' ]] || ln -s '/opt/puppetlabs/puppet/bin/wrapper.sh' '/opt/puppetlabs/bin/puppet') && \
	install -d '/opt/puppetlabs/bin' && \
	([[ '/opt/puppetlabs/bin/pxp-agent' -ef '/opt/puppetlabs/puppet/bin/wrapper.sh' ]] || ln -s '/opt/puppetlabs/puppet/bin/wrapper.sh' '/opt/puppetlabs/bin/pxp-agent')
	touch wrapper-script-install

wrapper-script-clean:
	[ -d ./ ] && cd ./ && /usr/bin/make clean
	[ -e wrapper-script-configure ] && rm wrapper-script-configure
	[ -e wrapper-script-build ] && rm wrapper-script-build
	[ -e wrapper-script-install ] && rm wrapper-script-install

wrapper-script-clobber: wrapper-script-clean
	[ -d ./ ] && rm -r ./
	[ -e wrapper-script-unpack ] && rm wrapper-script-unpack

module-puppetlabs-augeas_core: module-puppetlabs-augeas_core-install

module-puppetlabs-augeas_core-install:
	install -d -m '0755' '/opt/puppetlabs/puppet/vendor_modules' && \
	mv puppetlabs-augeas_core /opt/puppetlabs/puppet/vendor_modules/augeas_core && \
	rm -r /opt/puppetlabs/puppet/vendor_modules/augeas_core/.[!.]* 2>/dev/null
	touch module-puppetlabs-augeas_core-install

module-puppetlabs-augeas_core-clean:
	[ -d puppetlabs-augeas_core ] && cd puppetlabs-augeas_core && /usr/bin/make clean
	[ -e module-puppetlabs-augeas_core-configure ] && rm module-puppetlabs-augeas_core-configure
	[ -e module-puppetlabs-augeas_core-build ] && rm module-puppetlabs-augeas_core-build
	[ -e module-puppetlabs-augeas_core-install ] && rm module-puppetlabs-augeas_core-install

module-puppetlabs-augeas_core-clobber: module-puppetlabs-augeas_core-clean
	[ -d puppetlabs-augeas_core ] && rm -r puppetlabs-augeas_core
	[ -e module-puppetlabs-augeas_core-unpack ] && rm module-puppetlabs-augeas_core-unpack

module-puppetlabs-cron_core: module-puppetlabs-cron_core-install

module-puppetlabs-cron_core-install:
	install -d -m '0755' '/opt/puppetlabs/puppet/vendor_modules' && \
	mv puppetlabs-cron_core /opt/puppetlabs/puppet/vendor_modules/cron_core && \
	rm -r /opt/puppetlabs/puppet/vendor_modules/cron_core/.[!.]* 2>/dev/null
	touch module-puppetlabs-cron_core-install

module-puppetlabs-cron_core-clean:
	[ -d puppetlabs-cron_core ] && cd puppetlabs-cron_core && /usr/bin/make clean
	[ -e module-puppetlabs-cron_core-configure ] && rm module-puppetlabs-cron_core-configure
	[ -e module-puppetlabs-cron_core-build ] && rm module-puppetlabs-cron_core-build
	[ -e module-puppetlabs-cron_core-install ] && rm module-puppetlabs-cron_core-install

module-puppetlabs-cron_core-clobber: module-puppetlabs-cron_core-clean
	[ -d puppetlabs-cron_core ] && rm -r puppetlabs-cron_core
	[ -e module-puppetlabs-cron_core-unpack ] && rm module-puppetlabs-cron_core-unpack

module-puppetlabs-host_core: module-puppetlabs-host_core-install

module-puppetlabs-host_core-install:
	install -d -m '0755' '/opt/puppetlabs/puppet/vendor_modules' && \
	mv puppetlabs-host_core /opt/puppetlabs/puppet/vendor_modules/host_core && \
	rm -r /opt/puppetlabs/puppet/vendor_modules/host_core/.[!.]* 2>/dev/null
	touch module-puppetlabs-host_core-install

module-puppetlabs-host_core-clean:
	[ -d puppetlabs-host_core ] && cd puppetlabs-host_core && /usr/bin/make clean
	[ -e module-puppetlabs-host_core-configure ] && rm module-puppetlabs-host_core-configure
	[ -e module-puppetlabs-host_core-build ] && rm module-puppetlabs-host_core-build
	[ -e module-puppetlabs-host_core-install ] && rm module-puppetlabs-host_core-install

module-puppetlabs-host_core-clobber: module-puppetlabs-host_core-clean
	[ -d puppetlabs-host_core ] && rm -r puppetlabs-host_core
	[ -e module-puppetlabs-host_core-unpack ] && rm module-puppetlabs-host_core-unpack

module-puppetlabs-mount_core: module-puppetlabs-mount_core-install

module-puppetlabs-mount_core-install:
	install -d -m '0755' '/opt/puppetlabs/puppet/vendor_modules' && \
	mv puppetlabs-mount_core /opt/puppetlabs/puppet/vendor_modules/mount_core && \
	rm -r /opt/puppetlabs/puppet/vendor_modules/mount_core/.[!.]* 2>/dev/null
	touch module-puppetlabs-mount_core-install

module-puppetlabs-mount_core-clean:
	[ -d puppetlabs-mount_core ] && cd puppetlabs-mount_core && /usr/bin/make clean
	[ -e module-puppetlabs-mount_core-configure ] && rm module-puppetlabs-mount_core-configure
	[ -e module-puppetlabs-mount_core-build ] && rm module-puppetlabs-mount_core-build
	[ -e module-puppetlabs-mount_core-install ] && rm module-puppetlabs-mount_core-install

module-puppetlabs-mount_core-clobber: module-puppetlabs-mount_core-clean
	[ -d puppetlabs-mount_core ] && rm -r puppetlabs-mount_core
	[ -e module-puppetlabs-mount_core-unpack ] && rm module-puppetlabs-mount_core-unpack

module-puppetlabs-scheduled_task: module-puppetlabs-scheduled_task-install

module-puppetlabs-scheduled_task-install:
	install -d -m '0755' '/opt/puppetlabs/puppet/vendor_modules' && \
	mv puppetlabs-scheduled_task /opt/puppetlabs/puppet/vendor_modules/scheduled_task && \
	rm -r /opt/puppetlabs/puppet/vendor_modules/scheduled_task/.[!.]* 2>/dev/null
	touch module-puppetlabs-scheduled_task-install

module-puppetlabs-scheduled_task-clean:
	[ -d puppetlabs-scheduled_task ] && cd puppetlabs-scheduled_task && /usr/bin/make clean
	[ -e module-puppetlabs-scheduled_task-configure ] && rm module-puppetlabs-scheduled_task-configure
	[ -e module-puppetlabs-scheduled_task-build ] && rm module-puppetlabs-scheduled_task-build
	[ -e module-puppetlabs-scheduled_task-install ] && rm module-puppetlabs-scheduled_task-install

module-puppetlabs-scheduled_task-clobber: module-puppetlabs-scheduled_task-clean
	[ -d puppetlabs-scheduled_task ] && rm -r puppetlabs-scheduled_task
	[ -e module-puppetlabs-scheduled_task-unpack ] && rm module-puppetlabs-scheduled_task-unpack

module-puppetlabs-selinux_core: module-puppetlabs-selinux_core-install

module-puppetlabs-selinux_core-install:
	install -d -m '0755' '/opt/puppetlabs/puppet/vendor_modules' && \
	mv puppetlabs-selinux_core /opt/puppetlabs/puppet/vendor_modules/selinux_core && \
	rm -r /opt/puppetlabs/puppet/vendor_modules/selinux_core/.[!.]* 2>/dev/null
	touch module-puppetlabs-selinux_core-install

module-puppetlabs-selinux_core-clean:
	[ -d puppetlabs-selinux_core ] && cd puppetlabs-selinux_core && /usr/bin/make clean
	[ -e module-puppetlabs-selinux_core-configure ] && rm module-puppetlabs-selinux_core-configure
	[ -e module-puppetlabs-selinux_core-build ] && rm module-puppetlabs-selinux_core-build
	[ -e module-puppetlabs-selinux_core-install ] && rm module-puppetlabs-selinux_core-install

module-puppetlabs-selinux_core-clobber: module-puppetlabs-selinux_core-clean
	[ -d puppetlabs-selinux_core ] && rm -r puppetlabs-selinux_core
	[ -e module-puppetlabs-selinux_core-unpack ] && rm module-puppetlabs-selinux_core-unpack

module-puppetlabs-sshkeys_core: module-puppetlabs-sshkeys_core-install

module-puppetlabs-sshkeys_core-install:
	install -d -m '0755' '/opt/puppetlabs/puppet/vendor_modules' && \
	mv puppetlabs-sshkeys_core /opt/puppetlabs/puppet/vendor_modules/sshkeys_core && \
	rm -r /opt/puppetlabs/puppet/vendor_modules/sshkeys_core/.[!.]* 2>/dev/null
	touch module-puppetlabs-sshkeys_core-install

module-puppetlabs-sshkeys_core-clean:
	[ -d puppetlabs-sshkeys_core ] && cd puppetlabs-sshkeys_core && /usr/bin/make clean
	[ -e module-puppetlabs-sshkeys_core-configure ] && rm module-puppetlabs-sshkeys_core-configure
	[ -e module-puppetlabs-sshkeys_core-build ] && rm module-puppetlabs-sshkeys_core-build
	[ -e module-puppetlabs-sshkeys_core-install ] && rm module-puppetlabs-sshkeys_core-install

module-puppetlabs-sshkeys_core-clobber: module-puppetlabs-sshkeys_core-clean
	[ -d puppetlabs-sshkeys_core ] && rm -r puppetlabs-sshkeys_core
	[ -e module-puppetlabs-sshkeys_core-unpack ] && rm module-puppetlabs-sshkeys_core-unpack

module-puppetlabs-yumrepo_core: module-puppetlabs-yumrepo_core-install

module-puppetlabs-yumrepo_core-install:
	install -d -m '0755' '/opt/puppetlabs/puppet/vendor_modules' && \
	mv puppetlabs-yumrepo_core /opt/puppetlabs/puppet/vendor_modules/yumrepo_core && \
	rm -r /opt/puppetlabs/puppet/vendor_modules/yumrepo_core/.[!.]* 2>/dev/null
	touch module-puppetlabs-yumrepo_core-install

module-puppetlabs-yumrepo_core-clean:
	[ -d puppetlabs-yumrepo_core ] && cd puppetlabs-yumrepo_core && /usr/bin/make clean
	[ -e module-puppetlabs-yumrepo_core-configure ] && rm module-puppetlabs-yumrepo_core-configure
	[ -e module-puppetlabs-yumrepo_core-build ] && rm module-puppetlabs-yumrepo_core-build
	[ -e module-puppetlabs-yumrepo_core-install ] && rm module-puppetlabs-yumrepo_core-install

module-puppetlabs-yumrepo_core-clobber: module-puppetlabs-yumrepo_core-clean
	[ -d puppetlabs-yumrepo_core ] && rm -r puppetlabs-yumrepo_core
	[ -e module-puppetlabs-yumrepo_core-unpack ] && rm module-puppetlabs-yumrepo_core-unpack

module-puppetlabs-zfs_core: module-puppetlabs-zfs_core-install

module-puppetlabs-zfs_core-install:
	install -d -m '0755' '/opt/puppetlabs/puppet/vendor_modules' && \
	mv puppetlabs-zfs_core /opt/puppetlabs/puppet/vendor_modules/zfs_core && \
	rm -r /opt/puppetlabs/puppet/vendor_modules/zfs_core/.[!.]* 2>/dev/null
	touch module-puppetlabs-zfs_core-install

module-puppetlabs-zfs_core-clean:
	[ -d puppetlabs-zfs_core ] && cd puppetlabs-zfs_core && /usr/bin/make clean
	[ -e module-puppetlabs-zfs_core-configure ] && rm module-puppetlabs-zfs_core-configure
	[ -e module-puppetlabs-zfs_core-build ] && rm module-puppetlabs-zfs_core-build
	[ -e module-puppetlabs-zfs_core-install ] && rm module-puppetlabs-zfs_core-install

module-puppetlabs-zfs_core-clobber: module-puppetlabs-zfs_core-clean
	[ -d puppetlabs-zfs_core ] && rm -r puppetlabs-zfs_core
	[ -e module-puppetlabs-zfs_core-unpack ] && rm module-puppetlabs-zfs_core-unpack

module-puppetlabs-zone_core: module-puppetlabs-zone_core-install

module-puppetlabs-zone_core-install:
	install -d -m '0755' '/opt/puppetlabs/puppet/vendor_modules' && \
	mv puppetlabs-zone_core /opt/puppetlabs/puppet/vendor_modules/zone_core && \
	rm -r /opt/puppetlabs/puppet/vendor_modules/zone_core/.[!.]* 2>/dev/null
	touch module-puppetlabs-zone_core-install

module-puppetlabs-zone_core-clean:
	[ -d puppetlabs-zone_core ] && cd puppetlabs-zone_core && /usr/bin/make clean
	[ -e module-puppetlabs-zone_core-configure ] && rm module-puppetlabs-zone_core-configure
	[ -e module-puppetlabs-zone_core-build ] && rm module-puppetlabs-zone_core-build
	[ -e module-puppetlabs-zone_core-install ] && rm module-puppetlabs-zone_core-install

module-puppetlabs-zone_core-clobber: module-puppetlabs-zone_core-clean
	[ -d puppetlabs-zone_core ] && rm -r puppetlabs-zone_core
	[ -e module-puppetlabs-zone_core-unpack ] && rm module-puppetlabs-zone_core-unpack

cleanup: cleanup-install

cleanup-unpack: file-list-before-build
	: no source, so nothing to extract
	touch cleanup-unpack

cleanup-patch: cleanup-unpack
	touch cleanup-patch

cleanup-configure: cleanup-patch
	[ -d ./ ] || mkdir -p ./
	touch cleanup-configure

cleanup-build: cleanup-configure
	touch cleanup-build

cleanup-check: cleanup-build
	touch cleanup-check

cleanup-install: cleanup-check
	cd ./ && \
	rm -rf /opt/puppetlabs/puppet/include/augeas.h && \
	rm -rf /opt/puppetlabs/puppet/include/boost && \
	rm -rf /opt/puppetlabs/puppet/include/cpp-pcp-client && \
	rm -rf /opt/puppetlabs/puppet/include/fa.h && \
	rm -rf /opt/puppetlabs/puppet/include/facter && \
	rm -rf /opt/puppetlabs/puppet/include/hocon && \
	rm -rf /opt/puppetlabs/puppet/include/leatherman && \
	rm -rf /opt/puppetlabs/puppet/include/libexslt && \
	rm -rf /opt/puppetlabs/puppet/include/libxml2 && \
	rm -rf /opt/puppetlabs/puppet/include/libxslt && \
	rm -rf /opt/puppetlabs/puppet/include/whereami && \
	rm -rf /opt/puppetlabs/puppet/include/yaml-cpp && \
	rm -rf /opt/puppetlabs/puppet/ssl/man && \
	rm -rf /opt/puppetlabs/service_conf
	touch cleanup-install

cleanup-clean:
	[ -d ./ ] && cd ./ && /usr/bin/make clean
	[ -e cleanup-configure ] && rm cleanup-configure
	[ -e cleanup-build ] && rm cleanup-build
	[ -e cleanup-install ] && rm cleanup-install

cleanup-clobber: cleanup-clean
	[ -d ./ ] && rm -r ./
	[ -e cleanup-unpack ] && rm cleanup-unpack

pl-ruby-patch: pl-ruby-patch-install

pl-ruby-patch-unpack: file-list-before-build
	: no source, so nothing to extract
	touch pl-ruby-patch-unpack

pl-ruby-patch-patch: pl-ruby-patch-unpack
	touch pl-ruby-patch-patch

pl-ruby-patch-configure: pl-ruby-patch-patch
	[ -d ./ ] || mkdir -p ./
	touch pl-ruby-patch-configure

pl-ruby-patch-build: pl-ruby-patch-configure
	touch pl-ruby-patch-build

pl-ruby-patch-check: pl-ruby-patch-build
	touch pl-ruby-patch-check

pl-ruby-patch-install: pl-ruby-patch-check
	touch pl-ruby-patch-install

pl-ruby-patch-clean:
	[ -d ./ ] && cd ./ && /usr/bin/make clean
	[ -e pl-ruby-patch-configure ] && rm pl-ruby-patch-configure
	[ -e pl-ruby-patch-build ] && rm pl-ruby-patch-build
	[ -e pl-ruby-patch-install ] && rm pl-ruby-patch-install

pl-ruby-patch-clobber: pl-ruby-patch-clean
	[ -d ./ ] && rm -r ./
	[ -e pl-ruby-patch-unpack ] && rm pl-ruby-patch-unpack

clean: puppet-runtime-clean puppet-clean facter-clean hiera-clean puppet-resource_api-clean shellpath-clean wrapper-script-clean module-puppetlabs-augeas_core-clean module-puppetlabs-cron_core-clean module-puppetlabs-host_core-clean module-puppetlabs-mount_core-clean module-puppetlabs-scheduled_task-clean module-puppetlabs-selinux_core-clean module-puppetlabs-sshkeys_core-clean module-puppetlabs-yumrepo_core-clean module-puppetlabs-zfs_core-clean module-puppetlabs-zone_core-clean cleanup-clean pl-ruby-patch-clean

clobber: puppet-runtime-clobber puppet-clobber facter-clobber hiera-clobber puppet-resource_api-clobber shellpath-clobber wrapper-script-clobber module-puppetlabs-augeas_core-clobber module-puppetlabs-cron_core-clobber module-puppetlabs-host_core-clobber module-puppetlabs-mount_core-clobber module-puppetlabs-scheduled_task-clobber module-puppetlabs-selinux_core-clobber module-puppetlabs-sshkeys_core-clobber module-puppetlabs-yumrepo_core-clobber module-puppetlabs-zfs_core-clobber module-puppetlabs-zone_core-clobber cleanup-clobber pl-ruby-patch-clobber

.PHONY: clean clobber puppet-runtime-clean puppet-runtime-clobber puppet-clean puppet-clobber facter-clean facter-clobber hiera-clean hiera-clobber puppet-resource_api-clean puppet-resource_api-clobber shellpath-clean shellpath-clobber wrapper-script-clean wrapper-script-clobber module-puppetlabs-augeas_core-clean module-puppetlabs-augeas_core-clobber module-puppetlabs-cron_core-clean module-puppetlabs-cron_core-clobber module-puppetlabs-host_core-clean module-puppetlabs-host_core-clobber module-puppetlabs-mount_core-clean module-puppetlabs-mount_core-clobber module-puppetlabs-scheduled_task-clean module-puppetlabs-scheduled_task-clobber module-puppetlabs-selinux_core-clean module-puppetlabs-selinux_core-clobber module-puppetlabs-sshkeys_core-clean module-puppetlabs-sshkeys_core-clobber module-puppetlabs-yumrepo_core-clean module-puppetlabs-yumrepo_core-clobber module-puppetlabs-zfs_core-clean module-puppetlabs-zfs_core-clobber module-puppetlabs-zone_core-clean module-puppetlabs-zone_core-clobber cleanup-clean cleanup-clobber pl-ruby-patch-clean pl-ruby-patch-clobber

# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
CONFIGS_DIR = "configs.d"

require 'yaml'
require 'logger'

logger = Logger.new(STDOUT)
logger.level = Logger::WARN

def process_system(vag, sysconfig)
  if sysconfig["enabled"]
    vag.vm.define sysconfig["name"] do |system|
      system.vm.hostname = sysconfig["name"]
      system.vm.box = sysconfig["box"]
      
      system.vm.provider :virtualbox do |vb|
        vb.name = sysconfig["name"]
        vb.memory = sysconfig["ram"]
        vb.cpus = system["cpus"]
      end   
    end
  end
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |vag|

  # Loop through each file in the configuration directory
  Dir.foreach(CONFIGS_DIR).select { |f| !(f == '.' || f == '..') }.each do |yaml_file|
    begin
      
      # Load the configuration YAML
      sysconfig = YAML.load_file("#{CONFIGS_DIR}/#{yaml_file}")
      
      # If the configuration contains an array of systems
      if sysconfig.kind_of?(Array)
        sysconfig.each do |sub_sysconfig|
          process_system(vag, sub_sysconfig)
        end
      else
        process_system(vag, sysconfig)
      end
    rescue Exception => e
      puts "Error setting up configuration from #{yaml_file}"
      logger.error e.message
      e.backtrace.each { |line| logger.error line }
    end
  end
end

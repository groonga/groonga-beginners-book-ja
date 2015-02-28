require "yaml"

def base_dir
  File.expand_path(File.dirname(__FILE__))
end

def config_path
  File.join(base_dir, "config.yml")
end

def configurations
  @configurations ||= YAML.load(File.read(config_path))
end

namespace :generate do
  desc "generate HTML"
  task :html do |re_path|
    sh("review-compile", "--target=html", "--all")
  end

  desc "generate PDF"
  task :pdf do
    sh("review-pdfmaker", config_path)
  end

  desc "generate EPUB"
  task :epub do
    sh("review-epubmaker", config_path)
  end
end

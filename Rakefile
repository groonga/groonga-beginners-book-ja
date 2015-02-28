require "yaml"
require "rake/clean"

def base_dir
  File.expand_path(File.dirname(__FILE__))
end

def config_path
  File.join(base_dir, "config.yml")
end

def configurations
  @configurations ||= YAML.load(File.read(config_path))
end

def bookname
  configurations["bookname"]
end

CLEAN.include(FileList["*.html"])
CLEAN.include("#{bookname}-pdf/")
CLEAN.include("#{bookname}-epub/")
CLEAN.include(FileList["#{bookname}-*-*-*/"])
CLOBBER.include("#{bookname}.pdf")
CLOBBER.include("#{bookname}.epub")

namespace :generate do
  desc "generate HTML"
  task :html do |re_path|
    sh("review-compile", "--target=html", "--all")
  end

  desc "generate PDF"
  task :pdf do
    rm_rf("#{bookname}-pdf/")
    sh("review-pdfmaker", config_path)
  end

  desc "generate EPUB"
  task :epub do
    rm_rf("#{bookname}-epub/")
    sh("review-epubmaker", config_path)
  end
end

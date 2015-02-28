require "fileutils"
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

def bookname
  configurations["bookname"]
end

namespace :generate do
  desc "generate HTML"
  task :html do |re_path|
    system("review-compile", "--target=html", "--all")
  end

  desc "generate PDF"
  task :pdf do
    pdf_path = "#{bookname}.pdf"
    FileUtils.rm(pdf_path) if File.exist?(pdf_path)
    system("review-pdfmaker", config_path)
  end

  desc "generate EPUB"
  task :epub do
    system("review-epubmaker", config_path)
  end
end

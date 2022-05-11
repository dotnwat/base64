conf = configuration_data()

foreach codec : codecs
  name = 'HAVE_' + codec.to_upper()
  flags = get_option(f'@codec@_flags')
  conf.set10(name, flags.length() > 0)
endforeach

config_h = configure_file(output: 'config.h', configuration: conf)

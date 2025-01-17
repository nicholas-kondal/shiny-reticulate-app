# This file configures the virtualenv and Python paths differently depending on
# the environment the app is running in (local vs remote server).

# Edit this name if desired when starting a new app
VIRTUALENV_NAME = 'example_env_name'

# ------------------------- Settings (Edit local settings to match your system) -------------------------- #

if (Sys.info()[['user']] == 'shiny'){
  
  # Running on shinyapps.io
  Sys.setenv(PYTHON_PATH = 'python3')
  Sys.setenv(VIRTUALENV_NAME = VIRTUALENV_NAME) # Installs into default shiny virtualenvs dir
  Sys.setenv(RETICULATE_PYTHON = paste0('/home/shiny/.virtualenvs/', VIRTUALENV_NAME, '/bin/python'))
  
  # Verify Python path exists
  if (!file.exists(Sys.getenv('PYTHON_PATH'))) {
    warning("Python path not found at: ", Sys.getenv('PYTHON_PATH'))
    # Fallback to alternative Python path
    alternative_paths <- c(
      '/usr/bin/python3',
      '/opt/python/python3/bin/python',
      '/usr/bin/python3.12',
      '/opt/python/python3.12/bin/python',
      '/usr/bin/python3.11',
      '/opt/python/python3.11/bin/python',
      '/usr/bin/python3.10',
      '/opt/python/python3.10/bin/python',
      '/usr/bin/python3.9',
      '/opt/python/python3.9/bin/python',
      '/usr/bin/python3.8',
      '/opt/python/python3.8/bin/python',
      '/usr/bin/python3.7',
      '/opt/python/python3.7/bin/python'
    )
    
    for (path in alternative_paths) {
      if (file.exists(path)) {
        Sys.setenv(PYTHON_PATH = path)
        message("Using alternative Python path: ", path)
        break
      }
    }
  }
} else if (Sys.info()[['user']] == 'rstudio-connect'){
  
  # Running on remote server
  Sys.setenv(PYTHON_PATH = '/opt/python/3.7.7/bin/python3')
  Sys.setenv(VIRTUALENV_NAME = paste0(VIRTUALENV_NAME, '/')) # include '/' => installs into rstudio-connect/apps/
  Sys.setenv(RETICULATE_PYTHON = paste0(VIRTUALENV_NAME, '/bin/python'))
  
} else {
  
  # Running locally
  options(shiny.port = 7450)
  Sys.setenv(PYTHON_PATH = 'python3')
  Sys.setenv(VIRTUALENV_NAME = VIRTUALENV_NAME) # exclude '/' => installs into ~/.virtualenvs/
  # RETICULATE_PYTHON is not required locally, RStudio infers it based on the ~/.virtualenvs path
}

# Print environment variables for logging
message("Python Path: ", Sys.getenv('PYTHON_PATH'))
message("Virtualenv Name: ", Sys.getenv('VIRTUALENV_NAME'))
message("Reticulate Python: ", Sys.getenv('RETICULATE_PYTHON'))

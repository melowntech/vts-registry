set(registry_MAIN
  boundlayers.json
  credits.json
  referenceframes.json
  srs.json)

# install main registry files
install(FILES ${registry_MAIN}
  DESTINATION etc/registry
  COMPONENT main
  )

# install geoidgrid
install(DIRECTORY geoidgrid
  DESTINATION etc/registry
  COMPONENT main
  FILES_MATCHING PATTERN "*.jpg"
  )

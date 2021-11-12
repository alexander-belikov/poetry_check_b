# poetry_check_b

dummy package to demonstrate [Poetry issue 4723](https://github.com/python-poetry/poetry/issues/4723)

to check type `poetry update`

Current stack trace:

```shell
Updating dependencies
Resolving dependencies...
   1: fact: poetry-check-b is 0.2.0
   1: derived: poetry-check-b
   1: fact: poetry-check-b depends on poetry-check-a (rev main)
   1: selecting poetry-check-b (0.2.0)
   1: derived: poetry-check-a (1.0.1 git rev main)
   1: selecting poetry-check-a (1.0.1 1879bbc)
   1: Version solving took 5.569 seconds.
   1: Tried 1 solutions.

Finding the necessary packages for the current system

Package operations: 1 install, 0 updates, 0 removals

  - Installing poetry-check-a (1.0.1 1879bbc)

  Stack trace:

  18  ~/.local/lib/python3.8/site-packages/cleo/application.py:330 in run
       328│ 
       329│             try:
     → 330│                 exit_code = self._run(io)
       331│             except Exception as e:
       332│                 if not self._catch_exceptions:

  17  ~/.local/lib/python3.8/site-packages/poetry/console/application.py:180 in _run
       178│         self._load_plugins(io)
       179│ 
     → 180│         return super()._run(io)
       181│ 
       182│     def _configure_io(self, io: IO) -> None:

  16  ~/.local/lib/python3.8/site-packages/cleo/application.py:425 in _run
       423│                 io.set_input(ArgvInput(argv))
       424│ 
     → 425│         exit_code = self._run_command(command, io)
       426│         self._running_command = None
       427│ 

  15  ~/.local/lib/python3.8/site-packages/cleo/application.py:467 in _run_command
       465│ 
       466│         if error is not None:
     → 467│             raise error
       468│ 
       469│         return event.exit_code

  14  ~/.local/lib/python3.8/site-packages/cleo/application.py:451 in _run_command
       449│ 
       450│             if event.command_should_run():
     → 451│                 exit_code = command.run(io)
       452│             else:
       453│                 exit_code = ConsoleCommandEvent.RETURN_CODE_DISABLED

  13  ~/.local/lib/python3.8/site-packages/cleo/commands/base_command.py:118 in run
       116│         io.input.validate()
       117│ 
     → 118│         status_code = self.execute(io)
       119│ 
       120│         if status_code is None:

  12  ~/.local/lib/python3.8/site-packages/cleo/commands/command.py:85 in execute
        83│ 
        84│         try:
     →  85│             return self.handle()
        86│         except KeyboardInterrupt:
        87│             return 1

  11  ~/.local/lib/python3.8/site-packages/poetry/console/commands/update.py:49 in handle
        47│         self._installer.update(True)
        48│ 
     →  49│         return self._installer.run()
        50│ 

  10  ~/.local/lib/python3.8/site-packages/poetry/installation/installer.py:114 in run
       112│         local_repo = Repository()
       113│ 
     → 114│         return self._do_install(local_repo)
       115│ 
       116│     def dry_run(self, dry_run: bool = True) -> "Installer":

   9  ~/.local/lib/python3.8/site-packages/poetry/installation/installer.py:355 in _do_install
       353│ 
       354│         # Execute operations
     → 355│         return self._execute(ops)
       356│ 
       357│     def _write_lock_file(self, repo: Repository, force: bool = True) -> None:

   8  ~/.local/lib/python3.8/site-packages/poetry/installation/installer.py:409 in _execute
       407│ 
       408│         for op in operations:
     → 409│             self._execute_operation(op)
       410│ 
       411│         return 0

   7  ~/.local/lib/python3.8/site-packages/poetry/installation/installer.py:419 in _execute_operation
       417│         method = operation.job_type
       418│ 
     → 419│         getattr(self, f"_execute_{method}")(operation)
       420│ 
       421│     def _execute_install(self, operation: Install) -> None:

   6  ~/.local/lib/python3.8/site-packages/poetry/installation/installer.py:444 in _execute_install
       442│             return
       443│ 
     → 444│         self._installer.install(operation.package)
       445│ 
       446│     def _execute_update(self, operation: Update) -> None:

   5  ~/.local/lib/python3.8/site-packages/poetry/installation/pip_installer.py:40 in install
        38│ 
        39│         if package.source_type == "git":
     →  40│             self.install_git(package)
        41│ 
        42│             return

   4  ~/.local/lib/python3.8/site-packages/poetry/installation/pip_installer.py:266 in install_git
       264│         pkg.develop = package.develop
       265│ 
     → 266│         self.install_directory(pkg)
       267│ 

   3  ~/.local/lib/python3.8/site-packages/poetry/installation/pip_installer.py:204 in install_directory
       202│             # so we need to check the version of pip to know
       203│             # if we can rely on the build system
     → 204│             legacy_pip = self._env.pip_version < self._env.pip_version.__class__(
       205│                 19, 0, 0
       206│             )

   2  <string>:10 in __init__

   1  ~/.local/lib/python3.8/site-packages/poetry/core/version/pep440/version.py:44 in __post_init__
        42│         # we do this here to handle both None and tomlkit string values
        43│         object.__setattr__(
     →  44│             self, "text", self.to_string() if not self.text else str(self.text)
        45│         )
        46│ 

  AttributeError

  'int' object has no attribute 'to_string'

  at ~/.local/lib/python3.8/site-packages/poetry/core/version/pep440/version.py:113 in to_string
      109│         version_string = dash.join(
      110│             filter(
      111│                 bool,
      112│                 [
    → 113│                     self.release.to_string(),
      114│                     self.pre.to_string(short) if self.pre else self.pre,
      115│                     self.post.to_string(short) if self.post else self.post,
      116│                     self.dev.to_string(short) if self.dev else self.dev,
      117│                 ],
```

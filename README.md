# ansible-macos-dotfiles
Ansible role to manage personal dotfiles.

[![Build Status](https://img.shields.io/travis/feffi/ansible-macos-dotfiles.svg)](https://travis-ci.org/feffi/ansible-macos-dotfiles) [![Github All Releases](https://img.shields.io/github/downloads/feffi/ansible-macos-dotfiles/total.svg)](https://github.com/feffi/ansible-macos-dotfiles) [![GitHub forks](https://img.shields.io/github/forks/feffi/ansible-macos-dotfiles.svg?style=social&label=Fork)](https://github.com/feffi/ansible-macos-dotfiles) [![GitHub stars](https://img.shields.io/github/stars/feffi/ansible-macos-dotfiles.svg?style=social&label=Star)](https://github.com/feffi/ansible-macos-dotfiles) [![GitHub watchers](https://img.shields.io/github/watchers/feffi/ansible-macos-dotfiles.svg?style=social&label=Watch)](https://github.com/feffi/ansible-macos-dotfiles) [![Twitter Follow](https://img.shields.io/twitter/follow/feffi1.svg?style=social&label=Follow)](https://twitter.com/feffi1) [![License](http://img.shields.io/:license-mit-blue.svg)](https://github.com/feffi/ansible-macos-dotfiles/blob/master/LICENSE)

## Requirements
- Ansible 2.3

### ansible.cfg
```
hash_behaviour = merge
```

## Install
Just add the role to your ``requirements.yml`` file:
```yaml
- src: https://github.com/feffi/ansible-macos-dotfiles.git
  name: feffi.macos-dotfiles
```

## Role Variables
All role based variables are listed below, along with default values:

```yaml
macos_dotfiles:
  # Containment directory for pulled git repositories
  containment: "{{ ansible_env.HOME + '/dotfiles' }}"
  # Git repositories to pull
  repositories:
    - { # Target name of the repository
        name: "dotfiles",
        # URL of the repository
        url: "https://github.com/feffi/dotfiles.git",
        # Symlinks to create from this repository, defaults to src= repo, dest= ~
        symlinks: [
          { file: "LICENSE" },
          { file: "README" },
          { file: "test-dir", force: yes, owner: root, group: admin, mode: "0777" }
        ]
      }
```

## Dependencies
None.

## Example Playbook

```yaml
    - hosts: all
      vars:
        macos_dotfiles:
          # Containment directory for pulled git repositories
          containment: "{{ ansible_env.HOME + '/dotfiles' }}"
          # Git repositories to pull
          repositories:
            - { # Target name of the repository
                name: "dotfiles",
                # URL of the repository
                url: "https://github.com/feffi/dotfiles.git",
                # Symlinks to create from this repository, defaults to src= repo, dest= ~
                symlinks: [
                  { file: "LICENSE" },
                  { file: "README" },
                  { file: "test-dir", force: yes, owner: root, group: admin, mode: "0777" }
                ]
              }
      roles:
        - { role: feffi.macos-dotfiles }
```
Or with local parameters:

```yaml
    - hosts: all
      roles:
        - { role: feffi.macos-dotfiles,
            macos_dotfiles: {
              # Containment directory for pulled git repositories
              containment: "{{ ansible_env.HOME + '/dotfiles' }}",
              # Git repositories to pull
              repositories: [
                { # Target name of the repository
                  name: "dotfiles",
                  # URL of the repository
                  url: "https://github.com/feffi/dotfiles.git",
                  # Symlinks to create from this repository, defaults to src= repo, dest= ~
                  symlinks: [
                    { file: "LICENSE" },
                    { file: "README" },
                    { file: "test-dir", force: yes, owner: root, group: admin, mode: "0777" }
                  ]
                }
              ]
            }
          }
```

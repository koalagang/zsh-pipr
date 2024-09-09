# Zsh-pipr
Zsh-pipr is a tiny plugin that integrates [pipr](https://github.com/elkowar/pipr) with zsh.
Whilst there is a zsh script provided directly within the pipr repo,
this breaks syntax highlighting and, moreover, is not easy to install with plugin managers.

## Installation
First install `pipr`, as this is a dependency, then install zsh-pipr through a method of your choosing.

### Manual
Clone `https://github.com/koalagang/zsh-pipr.git` into a location of your choosing
and then `source /path/to/pipr.plugin.zsh` from your zshrc.

### Plugin manager
You should be able to use any zsh plugin manager. Feel free to open an issue about it if this doesn't work out with your
favourite plugin manager.

### Nix (home-manager)
You can use the zsh home-manager module with the `fetchFromGithub` fetcher to install zsh-pipr.

For example:

```nix
# include pkgs
{ pkgs, ... }:
{
  # make sure to install pipr
  home.packages = [ pkgs.pipr ];
  programs.zsh = {
    enable = true;
    plugins = [
      {
        name = "zsh-pipr";
        file = "pipr.plugin.zsh";
        src = pkgs.fetchFromGitHub {
          owner = "koalagang";
          repo = "zsh-pipr";
          rev = "62e4a240d4354ed90071d7007896efc15a2381db";
          hash = "sha256-zxu/uk/iL5jPHilnvhB647+2f4kC8KpAKDbvJPimy/0=";
        };
      }
    ];
  };
}
```

## Usage
Simply hit ctrl+p to open pipr with the current contents of the commandline. When you wish to leave pipr, hit ctrl+c and
you'll be returned to the commandline with any extra content you added whilst using pipr.

## Tips
- You may want to add `eval_environment = ["zsh", "-c"]` to `~/.config/pipr/pipr.toml` because pipr uses bash by default
- Avoid using interactive tools like fzf with pipr as this can lead to issues
- Pipr has a bunch of [cool features](https://github.com/elkowar/pipr?tab=readme-ov-file#usage) so consider checking those out

+++
title = "I'm switching to NixOS"
date = 2026-08-27
description = "why i'm switching to nix :p"
[taxonomies]
tags = ["nix", "NixOS", "Linux", "first post"]
+++

I'm switching to nix yay  

## why

I'm switching because I can.
*Also,* it's objectively better than arch.
There were *multiple* times when updating my system broke it.
**this doesn't happen with nix.** nix has atomic upgrades which mitigate this entirely.
additionally, with NixOS I can put all of my configuration, packages, WM, DE, editor dotfiles, etc. up on github.
(see my github [here](https://github.com/diflouroethane/nixos-dots).)

## the learning curve?

there is a ***huge*** learning curve associated with learning nix. you have to learn a *purely* functional
programming language, with a bunch of weird conventions. in fact, here is my `flake.nix` file from my [nixos dotfiles](https://github.com/diflouroethane/nixos-dots/blob/master/flake.nix)
```nix
{
	description = "A NixOS flake";
	inputs = {
 		nixpkgs.url = "github:NixOS/nixpkgs/nixos-26.05";
		nixpkgsnew.url = "github:NixOS/nixpkgs?rev=7525d999cd850b9a488817abc89c75dc733acf17";
		agenix.url = "github:ryantm/agenix";
		agenix.inputs.nixpkgs.follows = "nixpkgs";
		nvf.url = "github:notashelf/nvf";
    	nvf.inputs.nixpkgs.follows = "nixpkgs";

		nix-flatpak.url = "github:gmodena/nix-flatpak?ref=latest";

		blender-bin.url = "https://flakehub.com/f/edolstra/blender-bin/*";
		#noctalia = {

		#	url = "github:noctalia-dev/noctalia";
		#	inputs.nixpkgs.follows = "nixpkgs";
		#};
		home-manager = {
			url = "github:nix-community/home-manager/release-26.05";
			inputs.nixpkgs.follows = "nixpkgs";
		};

	};

	outputs = {self, nixpkgs,nixpkgsnew, home-manager, agenix, nvf, nix-flatpak, blender-bin, ...}@inputs: {
		
		nixosConfigurations.inspiron = nixpkgs.lib.nixosSystem {
			specialArgs = {inherit inputs;};
			modules = [
				./hosts/inspiron
				
				nix-flatpak.nixosModules.nix-flatpak
				agenix.nixosModules.default	
				home-manager.nixosModules.home-manager
				{
					home-manager.useGlobalPkgs = true;
					home-manager.backupFileExtension = "backup";
					home-manager.useUserPackages = true;
					home-manager.extraSpecialArgs = {inherit inputs;};
					home-manager.users.ethan = import ./hosts/inspiron/home.nix;
					home-manager.sharedModules = [nvf.homeManagerModules.default];
				}
			];
		};

		nixosConfigurations.otabello = nixpkgs.lib.nixosSystem {
		specialArgs = {inherit inputs;};

		modules = [
			./hosts/otabello

			# agenix.nixosModules.default
			home-manager.nixosModules.home-manager
			{
			home-manager = {
				useGlobalPkgs = true;
				backupFileExtension = "backup";
				useUserPackages = true;
				extraSpecialArgs = {inherit inputs;};
				sharedModules = [nvf.homeManagerModules.default];
			};
			}
		];
		};

		nixosConfigurations.tarraco = nixpkgs.lib.nixosSystem {
		specialArgs = {inherit inputs;};

		modules = [
			./hosts/tarraco

			home-manager.nixosModules.home-manager
			{
				home-manager = {
					useGlobalPkgs = true;
					backupFileExtension = "backup";
					useUserPackages = true;
					extraSpecialArgs = {inherit inputs;};
					users.dfe = ./hosts/tarraco/home.nix;
					sharedModules = [nvf.homeManagerModules.default];
				};
			}

		];
		};
		
		nixosConfigurations.iso = nixpkgs.lib.nixosSystem {
		specialArgs = {inherit inputs;};

		modules = [
			"${nixpkgs}/nixos/modules/installer/cd-dvd/installation-cd-minimal.nix"
			./hosts/iso
		];
		};
	};
}
```
woah. that's a lot, isn't it? most of this was taken/adapted from other people's configs, to suit my needs.

I don't have anything else to say about nix. it's good for my workflow, but it's not for everybody. I still reccommend people try it out, but each one to their own.


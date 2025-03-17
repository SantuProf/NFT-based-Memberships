// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

contract NFTMembership {
    string public name = "NFTMembership";
    string public symbol = "NFTM";
    uint256 private _tokenIdCounter;
    address public owner;

    mapping(uint256 => address) private _owners;
    mapping(address => uint256) private _balances;
    mapping(uint256 => bool) private _activeMemberships;

    event MembershipMinted(address indexed member, uint256 tokenId);
    event MembershipRevoked(uint256 tokenId);

    modifier onlyOwner() {
        require(msg.sender == owner, "Not contract owner");
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    function mintMembership(address to) external onlyOwner {
        uint256 tokenId = _tokenIdCounter;
        _tokenIdCounter++;
        _owners[tokenId] = to;
        _balances[to] += 1;
        _activeMemberships[tokenId] = true;
        emit MembershipMinted(to, tokenId);
    }

    function revokeMembership(uint256 tokenId) external onlyOwner {
        require(_owners[tokenId] != address(0), "Token does not exist");
        _activeMemberships[tokenId] = false;
        emit MembershipRevoked(tokenId);
    }

    function isMembershipActive(uint256 tokenId) external view returns (bool) {
        return _activeMemberships[tokenId];
    }

    function ownerOf(uint256 tokenId) external view returns (address) {
        return _owners[tokenId];
    }

    function balanceOf(address member) external view returns (uint256) {
        return _balances[member];
    }
}

# Simple-Poll-Survey
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract SimplePoll {
    string public question;
    string[] public options;
    mapping(uint256 => uint256) public votes;
    mapping(address => bool) public hasVoted;

    constructor(string memory _question, string[] memory _options) {
        question = _question;
        options = _options;
    }

    function vote(uint256 optionIndex) public {
        require(!hasVoted[msg.sender], "Already voted");
        require(optionIndex < options.length, "Invalid option");
        votes[optionIndex]++;
        hasVoted[msg.sender] = true;
    }

    function getVoteCount(uint256 optionIndex) public view returns (uint256) {
        return votes[optionIndex];
    }
}
